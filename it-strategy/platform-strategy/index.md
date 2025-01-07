# Platform Strategy

* A critical success factor for platforms is defining which aspectsc an be harmonized and which ones must be kept variable.
* A good platform takes a step in the background of the participant to participant interaction.
* How users acces your platform is at least as important as what's inside.

## Part I : Understanding platforms

When people say platform, they mean different things. That's why it's wise to first look at the history of platforms, catalog different types of platforms, and highlight their benefits.

### Chapter 1: Key properties of platforms

Properties:
* Platforms Elevate: A platforms creates an elevated layer that others can stand on.
* Platforms Enable: Platforms value by allowing participants ot benefit from the presence of others.
  * E.g buyers/sellers, creators/follows,
* Platforms Democratize: Platforms make it easiy for participants to join thanks to lower barriers.
  * E-Commerce platforms allows sellers easier to find markets, pay-what-you-use on cloud
* Platforms Self-Perpetuate: Platforms enabling exchange between participants (virtual/physical goods)
  * Network effect: More sellers attracts more buyers which again attracts more sellers
  * This compounds well with the "Enable" property. Easy entry makes sure nohing stands in the way.
* Platforms Accelerate: Platforms remove any blockers and heavy lifting, so participant can focus much more on value creating tasks and innovation. Things can go faster. Here is where one can focus their time on differentiating tasks.
* Platforms Don't Constrain: They don't limit or put unnecessary constrains on the participants.

#### Examples

* Automotive platforms: Same components and chassis used across models, along to create many different models with little redesign.
* E-commerce platforms: Online marketplaces where sellers and buyers can find each others, removing all the effort to create ways to find and iteract with each other. It connects sellers and buyers directly with each other. An online supermarket not, it's being the in between middleman.
* Media Platforms: Social media, they make it easy to create and share or follow and interact
* Cloud platforms: Bit like dcars, all this heavy lifiting engineering components eaily accessible.
* Business Platforms: Do what cloud platforms did for it. Applications that added capabilities for customization. See CRM, ERP, ...
  * Go SaaS
  * Allow for customization
  * Golden combination

### Chapter 2: The different types of platforms

![Platform Models](assets/platform_models.jpg)

| Model/Type | Examples | Value Proposition | Interaction | Implementation |
| ---        | ---      | ---               | ---         | ---            |
| Marketplace | Airbnb, Ebay, amazon | Facilitate Transactions | Browser, Mobile, App, API | Propriety |
| Base | Cloud Providers | Rapidly provision IT resources | Console, CLI, API, automation | Proprietary + OSS |
| Developer | Portals, cloud "wrappers" | Increase speed, reuse, governance | Portal, CLI | Composed from OSS |
| Business Capability | Allianz, Syncier, About You | Build an open ecosystem | APIs, Custom Integration | Proprietary, on top of base platforms |

Models can be combined.

* **Marketplace**: Platform allows for farmers market model
  * Participants: Sellers/Buyers
  * Platform Takes care of: Search, ads, reviews, ranking, fraud and maybe payments.
  * Platfrom benefits from: Not maintaing inventory and various ways to generate revenue through fees.
  * Considerations:
    * The positive feedback cycle between buyers/sellers also posses a chicken-egg problem when launching.
    * Flexibility in fees help in inventivicing the balance, if there is a lack of sellers, seller fees wont help.
    * There is a big "Winner takes all" issue
* **Base**:
  * Participants: Developers and IT professionals
  * Aim for feature parity across interaction channels (API, GUI, CLI, ...)
  * Reduce cognitive load for new platform users (reducing friction for new users).
  * How users acces your platform is at least as important as what's inside.
* **Developer**: In-House developer platforms are built by IT Departmens to provide reuse of common IT services, boost productivity and assure compliance with operational guidelines. Usually these are in support of the Software Development Lifecycle.
  * Sometimes these platforms create to much limitation that it defeats the purpose to be able to innovate.
* **Business Capability**: What a base platform is in business, delivering typical entire capabilities for business with the freedom to extendm customize and integrate with other systems via APIs.

## Part II: A Strategy for platforms

Building platforms requires a sizeable investment and a clear strategy. That strategy must turn the objectives into an actionable path defined by meaningful decisions.

### Chapter 3: Formulating a Strategy

#### What is Strategy
Strategy is not complex. But it is hard. It's hard because it forces people and organizations to make specific choices abotu their future - something that doesn't happen in most companies. Meaningful strategies must connect dots between long-term vision and short-ter, tactics, between busines and IT, and between quantifiable success metrics and beliefs. A strategy tells HOW to reach a goal, nut just list the goals.

A sound strategy depends on your organization's unique:
  * Assets: Brand, people, IP, Equipment, Cash, Technology,...
  * Constraints: Resources, Labor Contacts, Regulatory Environment, ...
  * Environment: Competitors, market positioning, price pressure, ...

Which also menas you can't copy someone else's strategy.

#### IT Strategy vs Business Strategy

* Historically IT strategy was basically "to accomedate the business" strategy, a one way street
* Nowadays technology can influence business strategy, we have two way street now
  * Some business strategies are only viable thanks to advances in technology
  * Technology allows now to sell extra services or charge "per consumption"
  * It is technology that enables new business strategy

#### Think in the First Derivative
Or: Think about how things change over time rather than focusing solely on their current state.

A platform strategy should think in the rate of change.

#### Documenting A Strategy

A good strategy consists of:
* Capturing key decisions
  * Covered in all the rest
* **Document them well**
  * Aim For Emphasis Over Completeness: Defining what's most relevant is a critical step towards devising a strategy.
    * See forest if you don't concern yourself with each tree, the real high level.
    * "What is not included" can be very useful chapter.
    * Remember, [clear writing](../../communication/writing.md)
  * Use Conceptual Models:
    * 2x2 matrixes, like SWOT
    * [See more on wikipedia](https://en.wikipedia.org/wiki/Conceptual_model) 
    * [Wardley Maps](https://en.wikipedia.org/wiki/Wardley_map)
  * Show the path and the terrain
    * A point: Where do you want to go? (+where you are?)
    * A Path: How will you get there?
    * A Terrain: What happens when you step of the path?
      * This shows how you see past happy-day scenarios

#### Credible roadmap

Simple linear road maps are unrealistic, foresee decision points, possible paths to be taken and the data needed to make those decisions.

![img](assets/strategic_roadmaps.png)

#### From Strategy to Execution

Take a list of all the "benefits" that you aim for and structure in a logical sequence of goals/mechanisms. An example structure that works:

1. **Context**: Explain why you are following a platform strategy. How does it align with the business strategy.
2. **Objectives**: The business benefits that are intended to be delivered by the strategy. Must be the **TOP Objectives**, not all benefits, less is more here.
  * E.g. Cost Reduction, faster innovation, ...
3. **Mechanisms**: Well-known techniques to deliver your objectives. Be very cautious to not just list buzzwords.
  * E.g. Increase code reuse, enable team autonomy
4. **Design Decisions**: Specific trade-offs that are made during implementation
  * E.g. All use the same programming language in return for x, y and Z

| **Level** | **Description** | **Key Activity** | **Example** |
| --- | --- | --- | --- |
| Context | Why you are create a strategy | Link to business | Increase Competition |
| Objective | What you want to achieve | Priorization | Speed up delivery |
| Mechanism | Common ways to get there | Translate Objectives |
| Design Decision | Trade-offs you are making | Explain Well | Standard APIs |

### Strategy is a Winding Road

A strategy is not a detailed plan but an overall direction.

### Chapter 4: Becoming a Platform Company
### Chapter 5: The Platform Paradox
### Chapter 6: Mappig Platforms
### Chapter 7: A Simple Framework For Writing IT Strategy
### Chapter 8: Case Stud - SIMBAS

## Part III: In-House platforms

Most IT organizations experience platforms when they set out to build one. This part looks beneath the covers of such platform initiatives to highlight important characteristics.

## Part IV: Designing platforms

Platforms hide complexity, but building one isn't nearly as simple as it looks from the outside. This part employs metaphors to illustrate platform design decisions.

## Part V: Implementing platforms

This part investigates platform anatomies and propose common platform blueprints.

## Part VI: Growing platforms

Platforms have to be rolled out across the organization. They also require delicate care and feeding over time so that they don't fall victim to excessive entropy or become a bottleneck. This part shows you how to do this successfully.

## Part VII: Organizing for platforms

If you are building platforms, you'll likely need a platform team, which is different from typical application delivery or operation teams. This part describes how to build an manage a platform team.

## Resources

* [Platform Strategy](https://leanpub.com/platformstrategy) by Gregor Hohpe
