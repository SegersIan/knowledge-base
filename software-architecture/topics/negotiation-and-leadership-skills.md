# Negotiation and Leadership Skill

These are hard skills to obtain. This topic cannot make you an expert overnight, the techniques introduced here are a good starting point for gaining these important skills. The reason we cover these skills is because a Software Architect must understand the political climate of the enterprise and navigate the politics. 

Reason being that almost every decision will be challenged. Developers that think they know more than the architect on a particular part, other architect who think they have a better approach, or business stakeholders that consider your decision to be too expensive. Your goal is not to go to war, but to find the best outcomes for the organization.

## Negotiation and Facilitation
Costs can be a deal breaker. You might need to hone your story and understanding to justify the cost. Else you might need to find alternatives that work better cost wise. Usually it is not binary a negotiation, but a conversation to find common ground and work within its boundaries. Remember, it's always about trade-offs.

**GENERAL TIP: Leave your ego at the door**

### Negotiating with Business Stakeholders

* **TIP: Leverage the use of grammar and buzzwords to better understand the situation**
    * Don't ignore the buzzwords or nonsense grammar, these give tremendous insights on what the concerns are from the business stakeholders, this allows you to better understand the real concerns. You can also use the same grammar and buzzwords to ask follow-up questions.
        * "I needed it yesterday" : Time To Market matters.
        * "It must be lightening fast" : Performance matters.
        * "I want 8 nines availability" : Availability matters.
* **TIP: Gather as much information as possible before entering into a negotiation**
    * This allows to navigate the negotiation in a constructive dialog. If you know the stakeholder mentioned they want "8 nines", have a table ready with the uptime percentage and the downtime per year/day which can help the stakeholder reflect the difference between 3 and 8 nines. Help them understand what they're really asking.
    * Having information at your finger tips allows for a constructive dialog. Do make sure to steer it in such a way.
* **TIP: When all else fails, state things in terms of cost and time**
    * This should be a last resort, starting of with "that's too expensive" can start of a negotiation of the wrong foot.
    * Ideally cost and time are considered once an agreement is reached and if they are relevant.
* **TIP: Leverage the "divide and conquer" rule to qualify demands or requirements**
    * Break down the demands or requirements, or consider adjusting scope.
    * Maybe the 8 nines are only relevant for a part of the system.
* **TIP: Prioritize strategically**
    * Stakeholders can "demand" certain features or functionality, or a solution to a problem that shouldn't exist in the first place. You can consider strategically focussing on the core of a problem, solve that, and then circle back to see if the need for given feature/requirement exists.
    * Example: Business stakeholders want a UI to change the behaviors/parameters of an automated cost approval. You can then focus first on designing and better analyzing the actual automation logic. When that is done (and maybe even delivered), you can circle back to ask, do you still need this UI? They might realize they don't need it at all. A way to deal with this is to plan the UI component later on the roadmap, so you can then gather feedback to see if if the concerns are still valid. After all, this is what being agile is about.

### Negotiating with Other Architects
Between architects the seniority can be in the way (ego), competitiveness, too argumentive, and could easily get personal. Some tips to deal with such situations.

* **TIP: Always remember that demonstration defeats discussion**
    * Every situation is different, just "googling it" doesn't exist, so every system is different.
    * Run a comparison between the competing options and show the results. 

* **TIP: Avoid being too argumentive or letting things get too personal in a negotiation - calm leadership combined with clear and concise reasoning will always win a negotiation.**
    * If things get too heated, park the discussion and come back at it later when all parties have calmed down.

### Negotiating with Developers
Don't leverage your title as architect to tell others what to do. Work with them and gain respect. Development teams can feel disconnected from architecture or the architect. As a result they feal out of the loop with regard to decisions that impact them. This is the manifestation of the **Ivory Tower Anti-Pattern**.

* **TIP: When convincing developers to adopt an architecture decision or to do a specific task, provide a justification rather than "dictating from on high".**
    * Developers care about "why", they don't like to be "just told what to do", you (as an architect) probably doesn't like it either.
    * Use of language: Don't use compelling speech (e.g. "You MUST...")

* **TIP: If a developer disagrees with a decision, have them arrive at the solution on their own.**
    * Tell the developer take their choice if they can "show" or "validate" (don't say proof) that their options does tackle concerns.
    * Example: The team will use Framework X if they can show how to address the security requirements"
        * Either the developers fails to show/validate this, so they come to their own conclusion, so you win their buy-in. That's a win.
        * Either the developers succeeds to show/validate this, that is still a win, the architect learns also something new, and the original concerns are addressed, so Framework X DOES seem to be the better option.

## The Software Architect as a Leader

50% about being an effective software architect is having good people skills, facilitation skills, and leadership skills. Here we cover some leadership techniques that you as an architect can leverage.

### The 4 C's of Architecture
Developers and architects love complexity. Developers are drawn to complexity like months to a flame, frequently with the same result. We have **essential complexity** (we have a hard problem), and we have **accidental complexity** (we have made a problem hard).

To avoid **accidental complexity** there is the 4 C's of architecture:
* **Communication**
* **Collaboration**
* **Conciseness**
* **Clarity**

These 4 factors work together to create an effective collaborator and communicator.

### Be Pragmatic, Yet Visionary

#### Visionary
> Thinking about or planning the future with imagination or wisdom.
> Being a visionary means applying strategic thinking to a problem.

#### Pragmatic
> Dealing with things sensibly and realistically in a way that is based on practical rather than theoretical considerations.

Being pragmatic is taking following factors and constraints in account when creating a solution:
* Budget constraints and other cost-based factors.
* Tome constraints and other time-based factors.
* Skill set and skill level of the development team.
* Trade-offs and implications associated with an architecture decision
* Technical limitations of a proposed architectural design or solution

#### Putting them together
Find an appropriate balance between being pragmatic while still applying imagination and wisdom to solving problems. Business stakeholders appreciate visionary solutions that fit within a set of constraints, and developers will appreciate having a practical (rather than theoretical solution to implement).

### Leading Teams By Example
Lead through example, not by title. This is the most efficient way to gather respect from others. Don't tell what and how it must be, ask questions, ask "what do you think of...", "have you considered", ... In coaching you help others find the questions, you don't tell them the solution.

Use people their names when you talk to them, it bonds and is more personal.

## Integrating with the Development Team

### Meetings
Key of being an effective software architect is making more time for the development team, this means controlling meetings.

* **Imposed Meetings (invited to a meeting)**:
    * Many invites are simply to keep you in the loop on information discussed, meeting notes are for that.
    * Ask for a meeting agenda ahead of time to help qualify if you are really needed at the meeting or not.
* **Imposes Meetings (you call the meeting)**
    * Keep to absolute minimum, especially with developers, respect their time and give them blocks of uninterrupted focus.
    * Often emails are enough to communicate.

### Others

* Sit with development teams physically.
* Block time to converse with the development teams.

## Resources

* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 23