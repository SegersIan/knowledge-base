# Event Versioning

## Why?

To avoid big bang releases.

## Rules

* A new version of an event must be convertible from the old version of the event. If not, it is not a new version of the event but rather a new event.d)
    * Any version of any event should be convertible from any version of a given event. If you find yourself trying to figure out how to convert your old event (Evil Kinevil jumping over a school bus on a motorcycle) to your new version of the event (a monkey eating a banana) and you can’t, this is because you have a new event and not a new version of it.
    * Following this rule you can always upcast.
* At any given point in time, you must only handle the version of the event you understand and ignore all others (to allow for Double Writes, so old and new version is published).


For most systems, a simple human-readable format such as json is fine for handling messages. Most production systems use mapping with either XML or json. Mapping with weak-schema will also remove many of the versioning problems associated with type-based strong schema discussed in the previous chapter.

There are scenarios where, either for performance reasons or in order to enable data to “pass through” without being understood, a wrapper may be a better solution than a mapping, but it will require more code. This methodology is, however, more common with messages, where an enrichment process is occurring, such as in a document-based system.

Overall though, there are very few reasons why it may be considered for the type-based mechanism. Once brought out of your immediate system and put into a serialized form, the type system does very little. The upcasting system is often difficult to maintain amongst consumers; even with a centralized schema repository, it requires another service. In most scenarios where messages are being passed to/from disparate services, late-binding tends to be a better option.

## General Tips

* Only having additive changes as opposed to destructive ones.

## Mapping Events Between Versions

You can do the mapping logic of an event between versions (e.g. OrderPlaced v1 and v2) on one of these two layers in your stack:
* **Data Layer**: You take an event stream and migrate/copy all this events into a new event stream with a new format. During this process, one can join/split streams and such if desired. This is like a traditional data migration of a database, without editing the table in place, but rather creating a new table where you copy the new version into. In the Application Layer the schema of the event has to be updated to reflect the schema of the new stream. 
* **Application Layer**: You don't change the original events but deal with versioning at run-time on application level.

## Versioning Approaches

| # | Name | Layer | Communication Direction |
| ---  | ---   | --- | --- |
| 1 | Strong Schema - Basic Type Based Versioning | Application | Uni-directional |
| 2 | Weak Schema - Mapping | Application | Uni-directional |
| 3 | Weak Schema - Wrapper | Application | Uni-directional |
| 4 | Negotiation | Application | Bi-directional |
| 5 | Copy and Replace | Data | Not Applicable |

### 1. Strong Schema - Basic Type Based Versioning

#### Description

* Assumes your serializer has no support for versioning.
* Explicit versions of a data schema are defined (e.g. v1, v2, ...)
* Data schema is expected to match 1:1 with the serialized type (e.g. WalletCreatedEvent).
* Multiple versions of a single schema are possible, but a type per version is required (e.g. WalletCreatedEvent_v1 and WalletCreatedEvent_v2).
* A new version of an event must be convertible from the old version of the event. If not, it is not a new version of the event but rather a new event.
* Upcasting logic : The logic to convert from an old to a new version is upcasting logic.
* The Ports/Adapters architecture allows you to decouple the version specific type (e.g. WalletCreatedEvent_v1) from your core business logic. Isolating your core from version changes. Alternatively you only pass the latest version (e.g. WalletCreatedEvent_latest), cause any old version should be able to be converted to the latest version.
* Double Publish: Avoid the issues that arise from having old consumers that do not understand the new version of the event. The idea is to have the new version of the producer write both the _v1 and the _v2 versions of the event when it writes. Downstream consumers can decide to ignore the newer version.

#### Pro
* todo...

#### Con
* If versions are not managed, it can become a mess (e.g. WalletCreatedEvent_v1 ... WalletCreatedEvent_v17) - method explosion in the upcasting logic.
* Serialize an Enum with a value that is not supported yet in the local strong schema requires dedicated logic.
* All consumers must be updated to understand the schema before a producer is updated.
* Upcasting is difficult to maintain.

### 2. Weak Schema - Mapping

#### Description

* Probably the better "Default" option.
* Assumes your serializer can have support for versioning.
* More rules that must be followed (than Strong Schema), it also offers more flexibility, providing the rules are followed.
* When mapping, you look at the json and at the instance:
    * Exists on json and instance -> value from json
    * Exists on json but not on instance -> NOP/Ignore
    * Exists on instance but not in json -> default value
* Only the current version of a data schema is defined (so no WalletCreatedEvent_v1 ... WalletCreatedEvent_v17, just WalletCreatedEvent).
    * That current version and the latest version are the same here, however that might not be reality.
* Data schema is **not** expected to match 1:1 with the serialized type (e.g. WalletCreatedEvent).
* Rule: You are no allowed to rename an attribute, unless you provide the old and name attribute with exact same value, but that translates in extra complexity, and is frankly, just annoying.
* Validation: You might need validation logic that validates if (after mapping) the mandatory fields are present/set and if to apply the correct defaults for absent fields.

#### Pro

* Relatively easy to implement with a "custom" JSON parser, default values, and/or a fluent API.


#### Con
* Serialize an Enum with a value that is not supported yet in the local strong schema requires dedicated logic.

### 3. Weak Schema - Wrapper

```
public class WalletCreatedEvent {
    private JObject _json;

    public WalletCreatedEvent(string json){
        _json = JObject.parse(json);
    }

    public Guid Id { 
        get {return Guid.Parse(_json["id"]);}
        set {_json["id"] = value.ToString();}
    }

    public string Name { 
        get {return _json["name"];}
        set {_json["name"] = value;}
    }   
}
```

#### Description

* Assumes your serializer can have support for versioning.
* More rules that must be followed (than Strong Schema), it also offers more flexibility, providing the rules are followed.
* In essence, you create a wrapper around the generic JSON object (e.g. JObject) with your Getters/Setters that either read/write the value from the JSON object at access time. In these Getter methods, logic can be placed for default values for missing fields.
* Only the current version of a data schema is defined (so no WalletCreatedEvent_v1 ... WalletCreatedEvent_v17, just WalletCreatedEvent).
    * That current version and the latest version are the same here, however that might not be reality.
* Data schema is **not** expected to match 1:1 with the serialized type (e.g. WalletCreatedEvent).
* Rule: You are no allowed to rename an attribute, unless you provide the old and name attribute with exact same value, but that translates in extra complexity, and is frankly, just annoying.


#### Pro
* Can serialize an Enum with a value that is not supported yet in the local strong schema.
* You can "pass through" the original JSON/XML and pass it on for serialization, this way, the entire original structure is kept that was not used by the internal model of that event in your service.
    * Common for document-based systems.

#### Con

* More work than Weak Schema - Mapper or Strong Schema.
* The internal implementation of the wrapper might warrant memory efficient implementation in high-performance systems (e.g. `JObject.Parse()` might not be most memory efficient)
* Some formats (e.g flatbutters) might only allow you to evolve a schema by appending to the end of the schema. (Such formats might be enforced by the need for efficient implementation).

### 4. Negotiation



#### Description

* Assumes Bi-Directional communications.
* We assume Atom Feeds as an example of this approach.
* Consumer can *negotiate* the format of the message which the message arrives in.
* Most common transport layer of such negotiation is HTTP.
* [Atom Feeds](https://datatracker.ietf.org/doc/html/rfc4287) are a good example of this.
* In a request a header can be used as `Accept: <some format>+<some version of the format>` (e.g. `Accept: WalletCreated_JSON+v2`).
* An atom feed response returns `uri's` which allows you to page through all events of a given stream. URIs will have the right parameters in the url regarding paging (e.g. `/stream/page_1`).
* TIP: You can implement this entire pattern on top of other transports, even message queues. The key is that the payload is not send via the main feed, but an URI/accessor instead.
    * e.g.
    ```
    WalletCreatedEvent{
        id: '<some-message-id>',
        type: 'WalletCreatedEvent',
        uri: '/messages/<some-message-id>'
    }
    ```
    * This allows for doing a GET request with content negotiation to the resource in desired format and version.
    * alternatively the message already exposed negotiation:
    ```
    WalletCreatedEvent{
        id: '<some-message-id>',
        type: 'WalletCreatedEvent',
        uri_json: '/messages/json/<some-message-id>',
        uri_xml: '/messages/xml/<some-message-id>'
    }
    ```
    * An announcement message is sent over the queue or previously over the Atom feed. Upon receipt of the announcement, the client must then fetch the message in the format they prefer. While quite flexible, this method is less than optimal in terms of performance, as it requires a request per message.
    * For scaling, there are methods for a consumer to pre register what content-types it is open to support, so not every request there is a content negotiation.
    * The producer will have to have downcast and/or upcast logic for the consumers and their requested type.
        * Limit the amount of supported versions to avoid version conversation code to blow up.

#### Pro

* The producer instead of all the consumers, must "know all formats and versions". The Consumers only their requested format and version of choice.
* Many of the URIs can be cached, allowing for easy scalability, cause there might be many consumers calling the producer.

#### Con

* More complex and effort.
* Requires some extra effort to optimize at high performance systems (e.g. negotiate in advance), but can work!

### 5. Copy And Replace

... todo

#### Description

#### Pro

#### Con

## General Concerns

### Versioning Of Behavior

If you find yourself putting branching logic or calculation logic in a projection, especially if it is based on time, you are probably missing logic in the creation of that event. A good example is the calculation of an invoice with Tax. The tax value might change over time. Make sure the event lists the tax value that was used, cause this value might change over time in the code. It may be worth including a description field even if only a string that describes the type of calculation made.

### Exterior Calls

Exterior calls are seldom idempotent. Try  to model the event post external call to contain all the information necessary so that downstream wise, you can replay with the result of the exterior call (e.g. PaymentSucceededEvent). Note that some information is just not allowed to be stored (credit card details).

A related problem to this happens when projections start doing lookups to other projections. If you find a projection making calls to external services or to other projections it will be a problem to replay later. As example there could be a customer table managed by a CustomerProjection and an orders table managed by an OrdersProjection. Instead of having the OrdersProjection listen to customer events the decision was made to have it lookup in the CustomerProjection what the current Customer Name is to copy into the orders table. This can save time and duplication in the OrdersProjection code.

### Changing Semantic Meaning

One important aspect of versioning is that semantic meaning cannot change between versions of software. There is no good way for a downstream consumer to understand a semantic meaning change. An example would be that the value for the `temperature` field went from Celsius to Fahrenheit.

### Snapshots

If you make snapshots for read efficiency, consider to still keep the original events, in case snapshots need to be regenerated or evolve over time.

In general, you can delete the old snapshots and then regenerate all snapshots based on updated logic/domain. If you need it side by side (an old an new version of a snapshot), regenerate the new snapshots and make sure you can handle both snapshot models in production. At a later stage the older snapshot model can be deprecated.

### Avoid "and"

If an event has "and" in the name (e.g. `TicketPaidForAndIssued`) consider to split into separate events. There is no need for a 1:1 relationship to "event received > process > output single event". Sometimes there are no output events necessary or multiple might.

## Resources

* [Versioning in an Event Sourced System - Gregory Young](https://leanpub.com/esversioning/read)