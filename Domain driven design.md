# Domain-driven design
Domain-driven design (DDD) is the concept that the structure and language of software code (class names, class methods, class variables) should match the business domain. 
For example, if a software processes loan applications, it might have classes such as LoanApplication and Customer, and methods such as AcceptOffer and Withdraw.

[Read more](https://en.wikipedia.org/wiki/Domain-driven_design)

## Kind of models

Domain-driven design recognizes multiple kinds of models.

* For example, an **entity** is an object defined not by its attributes, but its identity. As an example, most airlines assign a unique number to seats on every flight: this is 
the seat's identity.
* In contrast, a **value object** is an immutable object that contains attributes but has no conceptual identity. When people exchange business cards, for instance, they only 
care about the information on the card (its attributes) rather than trying to distinguish between each unique card.
* Models can also define events (something that happens). A domain event is an event that domain experts care about.
* Models can be bound together by a root entity to become an **aggregate**. Objects outside the aggregate are allowed to hold references to the root but not to any other object 
of the aggregate. The aggregate root checks the consistency of changes in the aggregate. Drivers do not have to individually control each wheel of a car, for instance: they 
simply drive the car. In this context, a car is an aggregate of several other objects (the engine, the brakes, the headlights, etc.)

### Entity
An object that is not defined by its attributes, but rather by a thread of continuity and its identity. 
* Attributes of the entity may change but the identity remains the same
* Mistaken identity can lead to data corruption.
* Define what it means to be the same thing (e.g. if two objects have the same type and id)

### Value Object
It describes a characteristic. It has no identity. \
It is an object that represents a descriptive aspect of the
domain with no conceptual identity. When you care only about the attributes of an element of the model:
* Address is a good candidate for a value object; it is entirely determined by its attributes.
* Money is another good example; each sum of equal value in the same currency are equal.
* Recipe ingredients might be a good example; you can use any actual ingredients, as long as they are the right type and quantity.

#### Example
Student is an entity \
Address is a value object

### Aggregates
Cluster the entities and value objects into aggregates and define boundaries around them. Choose one entity to be the root of each aggregate, and control access to the objects 
inside the boundary using the root. Allow external objects to hold references to the root only. \
e.g. - only StudentRepository, NOT AddressRepository.

### Data transfer objects
Data Transfer Objects (DTO) are object used to carry data between processes. In the case where communication between processes is expensive (e.g. over the Internet), it makes 
sense to bundle up the data and send it in one go. DTO's have no behaviour, they only contain data, so should not require testing
