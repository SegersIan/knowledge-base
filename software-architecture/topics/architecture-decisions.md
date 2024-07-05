# Architecture Decisions

Architecture decisions describe the **rules** for how a system should be constructed. These rules form the **constraints of the system** and **informs the developers on what they can and cannot do**.

Making architecture decisions involves gathering enough relevant information, justifying the decision, documenting the decision, and effectively communicating that decision to the right stakeholder.

Architectural decisions are about:
* **Making the right trade-offs** for your system. There is no perfect architecture, so we need to be explicit and conscious about which trade-offs we make. It's about **Fit For Purpose**.
    * Note that the [Software Architecture: The Hard Parts](https://architecturethehardparts.com/) books uses the following subtitle:
        > Modern Trade-Off analyses for Distributed Architectures.  
* **Keeping your options open** of your system in the future. 
    * Try to minimize the number of early and irreversible decisions. What we do is "defer" as many decisions as possible. When talking to business you could compare these "deferred decisions" to "options" in the finance.
    * Examples: Choosing a platform agnostic programming language, allow for horizontal scaling so the sizing decisions can be postponed (elasticity).
    * As Gregor Hohpe puts it: [Architecture is about selling options](https://architectelevator.com/architecture/architecture-options/).

[Architecture Decisions Example Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0105.png)

## Architecture Decision Anti-Patterns

As everywhere, anti-patterns tend to emerge. For architecture decisions, that's no different.

When making decisions the **Covering your Assets** anti-pattern usually occurs, overcoming this anti-pattern usually results in the **Groundhog Day** anti-pattern. Overcoming that anti-pattern leads to the **Email-Driven Architecture anti-pattern**. As an architect you need to overcome all 3 of these anti-patterns.


### Anti-Pattern: Covering your Assets

#### Cause
When an architects avoids or defers making an architecture decision out of fear of making the wrong choice.

#### Solution
* Wait until the last responsible moment to make an important architecture decision. This means waiting until you have enough information to justify and validate your decision, but not waiting so long that you hold up development teams or fall into the Analysis Paralysis anti-pattern.
* Continually collaborate with development teams to ensure that the decision you made can be implemented as expected.

### Anti-Pattern: Groundhog Day
#### Cause
When people don't know why a decision was made, so it keeps getting discussed over and over and over. This is because once an architect makes an architecture decision, they fail to provide a justification for the decision (or a complete justification).

#### Solution
* Provide both technical and business justifications for your decision.
* If a particular architecture decision does not provide any business value, then perhaps it is not a good decision and should be reconsidered.
* Most common business justifications include *cost, time to market, user satisfaction, and strategic positioning*. Take in consideration what is important for your stakeholder, maybe cost is less of a concern than time to market.


### Anti-Pattern: Email-Driven Architecture
#### Cause
Email is great for communicating, but is a poor document repository system.

#### Solution
* Do not include the architectural decision in the body of an email. Mention only the nature and the context of your decision in the body of the email and link to the system of record.
* Only notify people who care about the architectural decision.

> Hi Ian, an important decision regarding the architectural style was made that directly impacts you. Please see confluence page...link

## Technical Decisions

In general, technical decisions don't contain technological decisions. However, this is not always the case. If a specific technology is chosen because it directly supports a specific architectural characteristic, then it's an architecture decision.

## Architectural Decision Records (ADR)

One of the most effective ways of documenting architecture decisions. Evangelized by [Michael Nygard in a blog post](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions).

### Basic Structure
* **Title**: Number + Short description stating the architecture decision.
    * The numbering allows for easy reference.
* **Status**: State of the ADR
    * Status Types:
        * [Optional] RFC: Request for comments/feedback, advised is to set a deadline to avoid analysis paralysis
        * Proposed: Awaiting final approval
        * Accepted: Approved and ready for implementation
        * Superseded: Decision has been changed and superseded by another ADR. Powerful way to keep historical record of what decisions were made. It should point to the ADR/Decision it was superseded by.
    * Rules around status change can set who is allowed to approve what, based on *cost, cross-team impact, and security*. Based on the organization structure and who has a say in these factors, one can define who is allowed to approve decisions based on their impact.
* **Context**: What situation is forcing me to make this decision? Described the specific situation or issue and concisely elaborate on the possible alternatives. If required to document the analysis of each alternative in detail, consider adding an *Alternatives* section.
* **[Optional] Alternatives**: When desired, all the considered alternative solutions can be documented. 
* **Decision**: The *architecture decision + the full (technical and business) justification* for that decision. A *affirmative, demanding voice is advised* (e.g. "We will use..."). Emphasize on WHY the decision is made.
* **Consequences**: Document the overall impact of an architecture decision, good and bad. This should document the trade-off analysis associated with given decisions. This trade-off can be cost-based or against other architecture characteristics. It is important that we are explicit and understanding which trade-offs we make, making clear which concerns are more important than to others.
* **[Optional] Compliance**: Forces the architect to think about how the architecture decision will be measured and governed from a compliance perspective. Should this be a manual compliance check or can this be automated with a [*fitness function*](../topics/evolutionary-architecture.md#fitness-functions). The architect can document how this decision is enforced, if possible.
* **[Optional] Notes**:
    * Original Author
    * Approval Date
    * Approved By
    * Superseded date
    * Last modified date
    * Modified By

### Store ADRs

Based on the scope you should store these ADRs appropriately. You can store them in a git repo, close to the source, if the ADRs are scoped to everything that is located in that git repo. Alternatively, on larger scopes, consider shared folders (e.g. OneDrive) or CMS's.

## Exceptions

*An exception can be also named "a variance".*

There can be always a need for exceptions on any architectural decisions or rules. That is ok, this will always happen. However, you want to track and document these exceptions. See it as a "permit" to break a rule, that ideally must be explicitly approved. By documenting exceptions, one can track the *why* of the approval of the exception. If one would track the amount of exceptions, you can create more insight regarding your architectural decisions. Many exceptions can indicate that their might be issues with the existing rules/decisions. No exceptions can indicate that the rules/decisions are not relevant maybe or don't touch important subjects. As always, one would like to see a balance.


## Resources

* [GitHub ADR](https://adr.github.io/)
* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 19
* [ADR-Tools](https://github.com/npryce/adr-tools)
* [ADR-Tools Blog](https://www.hascode.com/2018/05/managing-architecture-decision-records-with-adr-tools/)
