# Domain Driven Design (DDD)

Domain-Driven-Design (DDD) is a popular and great logic design process to identify and define domains and their boundaries. [This is the original book](https://www.oreilly.com/library/view/domain-driven-design-tackling/0321125215/) and [this is a small martin fowler entry](https://martinfowler.com/bliki/DomainDrivenDesign.html). When reading about DDD, look for the **bounded contexts** parts which are great for domain modelling, DDD dus more than just that though.

## Event Storming

The architect tries to determine which events occur in the system based on requirements and identified roles, and build components around those event and message handlers. This works well in distributed architectures like microservices that use events and messages, because it helps architects define the messages used in the eventual system.