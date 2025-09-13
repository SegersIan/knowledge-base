# Making Development Teams Effective

Being able to make steams productive is one of the ways that software architects differentiate themselves from other software architects. Teams that feel left out of the loop or estranged from software architects (and also the architecture) often do not have the right level of guidance and right level of knowledge about various constraints on the system, and consequently do not implement the architecture correctly.

One of the roles of a software architect is to create and communicate constraints, or the box, in which developers can implement the architecture. ***Architects can create boundaries that are too tight, too lose, or just right.***

* **Too tight boundaries**: Causes *frustration* to the developers.
* **Too loose boundaries**: Creates *confusion* to the developers.
* **Appropriate boundaries**: Creates *effective* teams.

## Architect Personalities

* **Control Freak Architect**: Is one that defines **Too tight boundaries**
    * Too fine-grained or too low-level focus and decisions.
    * Steal the art of programming away.
    * Common mistake for anyone who just moved from development to architecture.
* **Armchair Architect**: Is one that defines  **Too loose boundaries**
    * Hasn't coded in a very long time (if at all) and doesn't take the implementation details in account when creating an architecture.
    * Disconnected from the teams.
    * Sometimes is in way over their head regarding the business domain or technology.
    * Architectures are often too high level, leaving too much up to the developers.
    * Indicators: 
        * Not having enough time (or choosing) to spend with the development teams.
        * Not fully understanding the business domain, business problem, or technology used.
        * Not enough hands-on experience developing software.
        * Not considering the implications associated with the implementation of the architecture solution.
* **Effective Architect**: Is one that defines  **Appropriate boundaries**
    * Requires working closely and collaborating with the team, and gaining the respect of the team as well. So, what is the right level of control to be effective?

## How Much Control?

To be an effective architect, knowing the right level of control to exert on a given development is key. This concept is known as [Elastic Leadership](https://www.elasticleadership.com/). Here we deviate a bit and focus on the specific factors for software architecture. There are 5 factors/dimensions that we influence the amount of control you ideally exert. The idea is that you quantify the team on these 5 factors to determine the level of control, or rather "what type of architect personality" you need to play. As a project progresses, these 5 factors will change over time. Therefore, periodically "measure" these 5 factors and adjust your level of control accordingly.

### Factors Impacting Control
* **Team Familiarity**: 
    * If members know each other, less control.
    * If members don't know each other, more control (to help facilitate collaboration between members).
* **Team Size**:
    * Smaller teams (4 or less), less control.
    * Bigger teams (12 or more), more control.
    * Note: Think of [Dunbar's Number](https://en.wikipedia.org/wiki/Dunbar%27s_number)
* **Overall Experience** in their career (junior/senior) or business domain
    * Few Juniors or familiar to business domain, less control (architect acts more as facilitator).
    * Many Juniors or new to business domain, more control (architect acts more as mentor).
* **Project Complexity**
    * Simple project, less control.
    * Complex project, more control (be more available and assist with issues)
* **Project Duration** 
    * Short project, less control.
    * Long project, more control.

### Determine Control
For each factor determine if it needs either less control (-20) also known as armchair architect, or more control (+20) also known as a control freak. Take the sum of all factors. The min value of the sum is `-100` (hardcore armchair) and the max sum is `+100` (hardcore control freak). Based on the sum you know if you need to be take a control freak (`>0`) or armchair role (`<0`) on a scale of 0 to 100.

### Example

| Factor                 | Value             | Rating  | Desired Role/Personality |
| ---                    | ---               | ---     | ---                      |
| **Team Familiarity**   | New team members  | +20     | Control Freak            |
| **Team Size**          | Small (4 members) | -20     | Armchair                 |
| **Overall Experience** | All experienced   | -20     | Armchair                 |
| **Project Complexity** | Relatively Simple | -20     | Armchair                 |
| **Project Duration**   | 2 months          | -20     | Armchair                 |
| **Accumulated score**  |                   | **-60** | **Armchair**             |

Obviously this is not an exact science, but rather a tool that just helps you guide the decision process.

## Team Warning Signs

3 factors come in place when considering the most effective development team size:

* **[Process Loss](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_2209.png)** (aka [Brook's Law](https://en.wikipedia.org/wiki/Brooks's_law)): The more people you add to a project, the more time it will take.
    * Actual productivity will always be less than the sum of all members potential (group potential). The difference between them being the process loss, caused by merge conflicts for example. If everyone is stepping on each others toes, the team might be too big.
* **Pluralistic Ignorance**: When everyone agrees to (but privately disagrees) a norm because they think they are missing the obvious (e.g. I guess I am the only one who doesn't get it, so I won't speak up, cause I might seem stupid or silly.). 
    * Pay attention to people's body language and facial expressions, ask people what they really think and support anyone speaking up.
* **Diffusion Of Responsibility**: As the team grows, the communication is negatively impacted.
    * Confusion about who is responsible for what on the team and things getting dropped are good sings the team is too large.
    * This get's very close to the [bystander effect](https://en.wikipedia.org/wiki/Bystander_effect).

## Leveraging Checklists

Surgeons and pilots use them, they work, they are very non-invasive tools to do a sanity check if something was overlooked. Even when repeating a process various times, the most experienced can overlook things.

As always, balance is key, too many checklists will loose its effect. Making checklists too long works also contra-productive.

**TIP: State also the obvious in checklist, its usually the obvious that is skipped or missed**.

A few example checklist that are proven to work:
* Developer Code Completion Checklist
* Unit and Functional Testing Checklist
* Software Release Checklist

## Resources

* [Checklist Manifesto](https://en.wikipedia.org/wiki/The_Checklist_Manifesto)
* [Dunbar's Number](https://en.wikipedia.org/wiki/Dunbar%27s_number)
* [Elastic Leadership](https://www.elasticleadership.com/)
* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 22