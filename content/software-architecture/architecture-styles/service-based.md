[<< Back To Overview](./readme.md)

# Architecture Style: Service-Based

![Service-Based Architecture Style Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1301.png)

## Description

Is a "hybrid" of the microservices architecture style. It's very pragmatic, flexible, but has one of the lowest complexity and cost of all distributed architecture style, making it a popular choice for business-related applications.

Basic topology of service-based architecture follows a distributed macro layered structure, consisting of a separately deployed user interface, distinct services, and a monolithic database. Services in this architecture are usually "domain services", covering a specific part of the general domain. All services are independent and separately deployed.

As a shared database is used, the number of services within an application context are generally between 4 and 12, averaging at 7 services.

Communication between the UI and the components usually are REST, RPC, SOAP, or messaging busses. Generally the user interface access the services directly using a [service locater pattern](https://en.wikipedia.org/wiki/Service_locator_pattern), API Gateway, or Proxy.

Due to the relative small amount of services, the DB connections are often not a bottleneck. Making changes however comes with challenges.

### Variants

This is a flexible architecture style, therefore many variants exist.

* [Break apart the User Interface](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1302.png)
* [Break apart the Database](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1303.png)
    * Important: There should not be data in a database that use used by other services, when partitioning to this degree. Nor redundant data. It is crucial to avoid interservice communication between services. If required, you might want to consider the microservice architecture style instead. 
* [Add an API layer](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1304.png)

These variants show that with this flexibility, one can design for scalability, fault tolerance, and security, by putting a specific database in a non public network.

### Difference with Microservice Architecture Style

In the Service Based Architecture style, all business logic is carefully located in a business domain, related to that domain. Therefore, a single (domain) service can use the ACID transaction properties for implementing any logic. Notice therefore, why in service based, interservice communication should be prohibited at all costs.

[Microservice Style](./microservices.md) allows interservice communication, meaning, that you loose the ACID transaction properties and depend on sagas and the BASE transaction properties. In Service based a single domain service would be responsible for example, an order, this OrderService would be responsible for the order, but also the payment and many other relevant responsibilities. In microservice style, these responsibilities would be most likely spread across multiple services.

Due to the limitation of no interservice communication, services are more "coarse-grained", meaning they take on more responsibility, are less "Specialized" and there might be duplication in functionality to avoid having to rely on interservice communication.

### Database Partitioning

As multiple services depend on the same, central, monolith database, it will be challenging to make changes to the databases while not causing problems for other services. Proper database partitioning is not mandatory, but can be of great help to mitigate some off these challenges.

In many languages you might have some "single shared library" with all the database entities that exist in your database. If one schema changes, this "single shared library" is updated, which causes ALL the domain services to be modified/affected. Hence, with logical portioning, you can have shared entity libraries and libraries per service domain, which decreases the impact of a single change to the database schema.

* [Single Shared Library Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1306.png)
* [Multiple Shared Library Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1306.png)

## When To Use

* Excellent architecture style which is flexible, use this when you a have bigger, more complex domain and application boundary. Yet, you don't want/cant afford the operational cost and technical challenges that other distributed architecture styles impose (e.g. Microservice style).
* Business application (landscapes) are usually a great fit.
* Natural fit for for DDD.


## When NOT To Use

* When you can't afford the cost, complexity, and skills that come with the more "fancy" and expansive distrusted architecture styles. It's not only about "not being able to afford", but also "Do I really need this high level of complexity". There is no shame in not taking the most "advanced" approach.

## Considerations

Important to read the **Difference with Microservice Architecture Style** note.

This is a lighter approach to microservice architecture style. It imposes some limits, it makes your services bigger, but you can work with plan old ACID transactions. Due to the imposed limitations, you take a lot of complexity of the table, which can be a key advantage. Working with fine-grained services comes with a whole set of challenges, which you might not want to tackle, or neither can afford their cost.

You have a distributed style, but transactions are contained within a single domain service, yet having high modularity and many other distributed advantages. You won't have to deal with "orchestration" or "choreography" for transactions across various fine grained services.

## Characteristics

| Characteristic    | Rating       |
| ---               | ---          |
| Partitioning Type | Domain    |
| Number of quanta  | 1 to many            |
| Deployability     | ⭐⭐⭐⭐           |
| Elasticity        | ⭐⭐           |
| Evolutionary      | ⭐⭐⭐           |
| Fault Tolerance   | ⭐⭐⭐⭐           |
| Modularity        | ⭐⭐⭐⭐           |
| Overall cost      | ⭐⭐⭐⭐ |
| Performance       | ⭐⭐⭐        |
| Reliability       | ⭐⭐⭐⭐      |
| Scalability       | ⭐⭐⭐           |
| Simplicity        | ⭐⭐⭐ |
| Testability       | ⭐⭐⭐⭐        |

## Resources

None