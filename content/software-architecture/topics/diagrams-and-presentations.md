# Diagramming and Presenting Architecture

Effective communication is critical to an architect's success. Diagramming and presenting are two critical soft skills for the software architect.

## Pattern: Representational Consistency
The practice of always showing the relationship between parts or an architecture, either in diagrams or presentations, before changing views. This is important when describing an architecture, where you must often show different views of the architecture.

[Diagram Example with Representational Consistency](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_2101.png)

## Diagramming
The topology of architecture is always of interest to architects and developers because if captures how the structure fits together.

### Anti-Pattern: Irrational Artifact Attachment
Proportional relationship between a person's irrational attachment to some artifact and how long it took to produce. That means one will be more attached to a four-hour diagram than a two-hour one. Using low-tech tools lets teams throw away what's not right. 

### Tool Requirements
Many tools exist, the following requirements are well advised to be productive and efficient in creating diagrams.

* **Layers**: A layer allows the drawer to link a group of items together logically to enable hiding/showing individual layers. Using layers, you can build a comprehensive diagram but hide overwhelming details when they aren't necessary.
* **Stencils/Templates**: Ability to build up a library of stencils/templates of common visual components, often composites of other basic shapes. This allows to create visual consistency within your organization.
* **Magnets**: Represents the places on those shapes where lines snap to connect automatically, providing automatic alignment and other visual niceties.

### Standards

* **UML**: Unified Modeling Language which has many interesting diagram types byt has fallen into disuse. Class and workflow diagrams are probably still most mainstream.
* **C4**: There are 4 views or "layers" of the system
    * *Context*: Entire context of the system, including the roles of users and external dependencies.
    * *Container*: The physical (and often logical) deployment boundaries and containers within the architecture. This view forms a good meeting point for operations and architects.
    * *Component*: This mostly aligns with an architect's view of the system.
    * *Class*: Same as the style of class diagrams from UML.
    * One downside is the inability  to express every kind of design an architecture might undertake. **C4 is best suited for monolithic architectures where the container and component relationships may differ, and it's less suited to distributed architectures.**
* **[ArchiMate](https://www.opengroup.org/archimate-forum/archimate-overview)**: Open source enterprise architecture modeling language to support the description, analysis, and visualization of architecture within and across business domains. The goal of ArchiMate is to be "as small as possible", not to cover every edge case scenario.

### Guidelines

When modelling, build your own style when creating diagrams and feel free to borrow from representations that are particularly effective.

* **Consistency**: Consistency is key
* **Titles**: All the elements of a diagram should have titles or are well known to the audience.
* **Lines**: Should be thick enough to see well. 
    * If lines indicate information flow, use arrows to indicate direction.
    * Different arrow heads might suggest other semantics, be consistent.
    * Sync communication is usually a solid line.
    * Async communication is usually a dotted line.
* **Shapes**: No shapes exists across software development, be consistent within your organization.
* **Labels**: Label each item.
* **Color**: We might often favour monochrome, use color when it helps distinguish artifacts from another.
* **Keys**: If shapes are ambiguous for any reason, include keys to indicate what each shape indicates. (a legend)

## Presenting

We will cover here a few interesting points, but the [Presentation Patterns](https://presentationpatterns.com/) book goes very deep here to list various patterns and anti-patterns.

The difference between a document and a presentation is ***time***, the presenter controls how quickly unfolds, instead of the the reader (which is the case with a document). Therefore, as a presenter you must learn how to *manipulate time*.

### Manipulating Time
Presentation tools offer 2 ways to manipulate time on slides: transitions and animations. Transitions move from slide to slide, animations allow for movement within a slide. These are used to hide the boundaries between slides. Using subtle combinations of transitions and animations such as dissolve allows presenters to hide individual slide boundaries, stitching together a set of slides to tell a single story. TO indicate the end of a thought, presenters should use a distinctly different transition (like a door or cube) to provide a visual clue tha they are move to a different topic.

### Incremental Builds
A common anti-pattern of presentations is where every slide has essentially the speaker's notes, projected for all to see. Most readers who read ahead of the speaker and then switch to listening, just waiting for the speaker to finish reading off the slide. Also this overloads the slide, which can be overload the attention of the audience.

The speaker has 2 information channels: verbal and visual. The solution to this problem is to use incremental builds for slides, building up (hopefully graphical) information as needed rather than all at once. 

You can use the same image but only show a part of it, and hide the rest of the image with a borderless white box. The presenter can then expose a portion at a time.

* [Bad Version: Slide shows everything at once](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_2101.png) - This can really be hard for anyone to process the image.
* [Good Version: Slide shows incrementally unveils part of the image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_2101.png) - This allows for a paced progression, unveiling one portion at a time. Building incrementally your story.

### Infodecks vs Presentations

* **Infodecks**: Slide decks that are not meant to be projected/presented but rather summarize information graphically. There is no need for transitions and animations, the information is also more comprehensive. All information should be on the slides, as they stand on their own. 
* **Presentations**: Slide deck meant for a presentation, where the presenter has a verbal and visual communication channel. Slides should be less comprehensive, as the verbal channel should guide through the presentation. Slides should be just half of the story.

### Slides Are Half Of The Story
Presenters make the mistake of adding too much material to slides when they can make important points more powerfully. Remember, presenters have 2 information channels (slides and speaker), use it strategically for adding more punch.

### Invisibility
A simple pattern where the presenter inserts a blank black slide within a presentation to refocus attention solely on the speaker. If someone has 2 information channels (slides and speaker) and turns one of them off (the slides), it automatically will focus attention back on the speaker because they are now the only interesting thing in the room to look at.

## Resources

* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 21
* [Presentation Patterns: Techniques of crafting better presentations](https://presentationpatterns.com/)