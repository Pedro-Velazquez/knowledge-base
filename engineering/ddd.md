# Domain-Driven Design

## Business domain/subdomain

A business domain defines a company’s main area of activity. Generally speaking, it’s the service the company provides to its clients. A company can operate in multiple business domains. It’s important to note that companies may change their business domains often.

To achieve its business domain’s goals and targets, a company has to operate in multiple subdomains. A subdomain is a fine-grained area of business activity. All of a company’s subdomains form its business domain: the service it provides to its customers. Implementing a single subdomain is not enough for a company to succeed; it’s just
one building block in the overarching system. The subdomains have to interact with each other to achieve the company’s goals in its business domain.

### Types of subdomain

* Core: A core subdomain is what a company does differently from its competitors. This may involve inventing new products or services or reducing costs by optimizing existing processes.
* Generic: Generic subdomains are business activities that all companies are performing in the same way. Like core subdomains, generic subdomains are generally complex and hard to implement. However, generic subdomains do not provide any competitive edge for the company. There is no need for innovation or optimization here: battletested implementations are widely available, and all companies use them.
* Supporting: As the name suggests, supporting subdomains support the company’s business. However, contrary to core subdomains, supporting subdomains do not provide any competitive advantage. Supporting subdomains are simple. Their business logic resembles mostly data entry screens and ETL (extract, transform, load) operations; that is,
the so-called CRUD (create, read, update, and delete) interfaces. These activity areas do not provide any competitive advantage for the company, and therefore do not require high entry barriers.

### Domain expert

Domain experts are subject matter experts who know all the intricacies
of the business that we are going to model and implement in code. In other words, domain experts are knowledge authorities in the software’s business domain. The domain experts are neither the analysts gathering the requirements nor the engineers designing the system. Domain experts represent the business. They are the people who identified the business problem in the first place and from whom all business knowledge originates. Systems analysts and engineers are transforming their mental
models of the business domain into software requirements and source code.

## Knowledge crunching

Effective domain modelers are knowledge crunchers. They take a torrent of information and probe for the relevant trickle. They try one organizing idea after another, searching for the simple view that makes sense of the mass. Many models are tried and rejected or transformed. Success comes in an emerging set of abstract concepts that makes sense of all the detail. This distillation is a rigorous expression of the particular knowledge that has been found most relevant.

Knowledge crunching is not a solitary activity. A team of developers and domain experts collaborate, typically led by developers. Together they draw in information and crunch it into a useful form. The raw material comes from the minds of domain experts, from users of existing systems, from the prior experience of the technical team with a related legacy system or another project in the same domain. It comes in the form of documents written for the project or used in the business, and lots and lots of talk. Early versions or prototypes feed experience back into the team and change interpretations.

Business activities and rules are as central to a domain as are the entities involved; any domain will have various categories of concepts. Knowledge crunching yields models that reflect this kind of insight. In parallel with model changes, developers refactor the implementation to express the model, giving the application use of that knowledge.

It is with this move beyond entities and values that knowledge crunching can get intense, because there may be actual inconsistency among business rules. Domain experts are usually not aware of how complex their mental processes are as, in the course of their work, they navigate all these rules, reconcile contradictions, and fill in gaps with common sense. Software can’t do this. It is through knowledge crunching in close collaboration with software experts that the rules are clarified, fleshed out reconciled, or placed out of scope.

### Tips for effective knowledge crunching

* Bind the model and the implementation.
* Cultivate a language based on the model.
* Develop a knowledge-rich model.
* Distill the model.
* Brainstorming and experimenting.

## Ubiquitous language

A domain model can be the core of a common language for a software project. The model is a set of concepts built up in the heads of people on the project, with terms and relationships that reflect domain insight. These terms and interrelationships provide the semantics of a language that is tailored to the domain while being precise enough for technical development. This is a crucial cord that weaves the model into development activity and binds it with the code.

This model-based communication is not limited to diagrams in Unified Modeling Language (UML). To make most effective use of a model, it needs to pervade every medium of communication. It increases the utility of written text documents, as well as the informal diagrams and casual conversation reemphasized in Agile processes. It improves communication through the code itself and through the tests for that code.

Domain experts have limited understanding of the technical jargon of software development, but they use the jargon of their field—probably in various flavors. Developers, on the other hand, may understand and discuss the system in descriptive, functional terms, devoid of the meaning carried by the experts’ language. Or developers may create abstractions that support their design but are not understood by the domain experts. Developers working on different parts of the problem work out their own design concepts and ways of describing the domain.

A project needs a common language that is more robust than the lowest common denominator. With a conscious effort by the team, the domain model can provide the backbone for that common language, while connecting team communication to the software implementation. That language can be ubiquitous in the team’s work.

The model-based language should be used among developers to describe not only artifacts in the system, but tasks and functionality. This same model should supply the language for the developers and domain experts to communicate with each other, and for the domain experts to communicate among themselves about requirements, development planning, and features. The more pervasively the language is used, the more smoothly understanding will flow.

## Building blocks

### Entities

An object defined primarily by its identity is called an Entity. Entities have special modeling and design considerations. They have life cycles that can radically change their form and content, but a thread of
continuity must be maintained. Their identities must be defined so that they can be effectively tracked. Their class definitions, responsibilities, attributes, and associations should revolve around who they are, rather than the particular attributes they carry. Even for Entities that don’t transform so radically or have such complicated life cycles, placing them in the semantic category leads to more lucid models and more robust implementations.

W hen an object is distinguished by its identity, rather than its attributes, mak e this primary to its definition in the model. Keep the class definition simple and focused on life cycle continuity and identity. Define a means of distinguishing each object regardless of its form or history. Be alert to requirements that call for matching objects
by attributes. Define an operation that is guaranteed to produce a unique result for each object, possibly by attaching a symbol that is guaranteed unique. This means of identification may come from the outside, or it may be an arbitrary identifier created by and for the system, but it must correspond to the identity distinctions in the model.
The model must define what it means to be the same thing.

It is natural to think about the attributes when modeling an object, and it is quite important to think about its behavior. But the most basic responsibility of Entities is to establish continuity so that behavior can be clear and predictable. They do this best if they are kept spare. Rather than focusing on the attributes or even the behavior, strip the Entity object’s definition down to the most intrinsic characteristics, particularly those that identify it or are commonly used to find or match it. Add only behavior that is essential to the concept and
attributes that are required by that behavior. Beyond that, look to remove behavior and attributes into other objects associated with the core Entity.

### Value objects

An object that represents a descriptive aspect of the domain with no conceptual identity is called a Value Object. Value Object are instantiated to represent elements of the design that we care about only for what they are, not who or which they are.

Defining Value Objects and designating them as immutable is a case of following a general rule: Avoiding unnecessary constraints in a model leaves developers free to do purely technical performance tuning. Explicitly defining the essential constraints lets developers tweak the design while keeping safe from changing meaningful behavior. Such design tweaks are often very specific to the technology in use on a particular project.

### Services

A Service is an operation offered as an interface that stands alone in the model, without encapsulating state, as Entities and Value Objects do. Services are a common pattern in technical frameworks, but they
can also apply in the domain layer.

The name service emphasizes the relationship with other objects. Unlike Entities and Value Objects, it is defined purely in terms of what it can do for a client. A Service tends to be named for an activity, rather than
an entity—a verb rather than a noun. A Service can still have an abstract, intentional definition; it just has a different flavor than the definition of an object. A Service should still have a defined responsibility, and that responsibility and the interface fulfilling it should be defined as part of the domain model. Operation names
should come from the UBIQUITOUS LANGUAGE or be introduced into it. Parameters and results should be domain objects.

A good Service has three characteristics.

* The operation relates to a domain concept that is not a natural part of an Entity or Value Object.
* The interface is defined in terms of other elements of the domain model.
* The operation is stateless.

Statelessness here means that any client can use any instance of a particular Service without regard to the instance’s individual history. The execution of a Service will use information that is accessible globally, and may even change that global information (that is, it may have side effects). But the Service does not hold state of its own that affects its own behavior, as most domain objects do. When a significant process or transformation in the domain is not a natural responsibility of an Entity or Value Object, add an operation to the model as a
standalone interface declared as a Service. Define the interface in terms of the language of the model and mak e sure the operation name is part of the Ubiquitous Language. Make the Service stateless.

### Aggregates

An Aggregate is a cluster of associated objects that we treat as a unit for the purpose of data changes. Each Aggregate has a root and a boundary. The boundary defines what is inside the Aggregate. The root is a single, specific Entity contained in the Aggregate. The root is the only member of the Aggregate that outside objects are allowed to hold references to, although objects within the boundary may hold references to each other. Entities other than the root have local identity, but that identity needs to be distinguishable only within the Aggregate, because no outside object can ever see it out of the context of the root Entity.

Invariants, which are consistency rules that must be maintained whenever data changes, will involve relationships between members of the Aggregate. Any rule that spans Aggregates will not be expected
to be up-to-date at all times. Through event processing, batch processing, or other update mechanisms, other dependencies can be resolved within some specified time. But the invariants applied within an Aggregate will be enforced with the completion of each transaction.

Rules to implement Aggregates:

* The root Entity has global identity and is ultimately responsible for checking invariants.
* Root Entities have global identity. Entities inside the boundary have local identity, unique only within the Aggregate.
* Nothing outside the Aggregate boundary can hold a reference to anything inside, except to the root Entity. The root Entity can hand references to the internal Entities to other objects, but those objects can use them only transiently, and they may not hold on to the reference. The root may hand a copy of a Value Object to another object, and it doesn’t matter what happens to it, because it’s just a Value and no longer will have any association with the Aggregate.
* As a corollary to the previous rule, only Aggregate roots can be obtained directly with database queries. All other objects must be found by traversal of associations.
* Objects within the Aggregate can hold references to other Aggregate roots.
* A delete operation must remove everything within the Aggregate boundary at once. (With garbage collection, this is easy. Because there are no outside references to anything but the root, delete the root
and everything else will be collected.)
* When a change to any object within the Aggregate boundary is committed, all invariants of the whole Aggregate must be satisfied.

Cluster the Entities and Value Objects into Aggregates and define boundaries around each. Choose one Entity to be the root of each Aggregate, and control all access to the objects inside the boundary through the root. Allow external objects to hold references to the root only. Transient references to internal members can be passed out for use within a single operation only. Because the root controls access, it cannot be blindsided by changes to the internals. This arrangement makes it practicalto enforce all invariants for objects in the Aggregate and for the Aggregate as a whole in any state change.

### Factory

A program element whose responsibility is the creation of other objects is called a Factory. Just as the interface of an object should encapsulate its implementation, thus allowing a client to use the object’s behavior without knowing how it works, a Factory encapsulates the knowledge needed to create a complex object or Aggregate. It provides an interface that reflects the goals of the client and an abstract view of the created object.

Shift the responsibility for creating instances of complex objects and Aggregates to a separate object, which may itself have no responsibility in the domain model but is still part of the domain design. Provide an interface that encapsulates all complex assembly and that does not require the client to reference the concrete classes of the objects
being instantiated. Create entire Aggregates as a piece, enforcing their invariants.

Basic requirements for a factory:

* Each creation method is atomic and enforces all invariants of the created object or Aggregate. A Factory should only be able to produce an object in a consistent state. For an Entity, this means the creation of the entire Aggregate, with all invariants satisfied, but probably with
optional elements still to be added. For an immutable Value Object, this means that all attributes are initialized to their correct final state. If the interface makes it possible to request an object that can’t be created correctly, then an exception should be raised or some other mechanism should be invoked that will ensure that no improper return value is possible.
* The Factory should be abstracted to the type desired, rather than the concrete class(es) created.

A Factory is very tightly coupled to its product, so a Factory should be attached only to an object that has a close natural relationship with the product. When there is something we want to hide—either the concrete implementation or the sheer complexity of construction—yet there doesn’t seem to be a natural host, we must create a dedicated Factory object or Service. A standalone Factory usually produces an entire Aggregate, handing out a reference to the root, and ensuring that the product Aggregate's invariants are enforced. If an object interior to an Aggregate needs a Factory, and the Aggregate root is not a reasonable home for it, then go ahead and make a standalone Factory. But respect the rules limiting access within an Aggregate, and make sure there are only transient references to the product from outside the Aggregate.

### Repository

A Repository represents all objects of a certain type as a conceptual set (usually emulated). It acts like a collection, except with more elaborate querying capability. Objects of the appropriate type are added and removed, and the machinery behind the Repository inserts them or deletes them from the database. This definition gathers a cohesive set of responsibilities for providing access to the roots of Aggregates from
early life cycle through the end.

Clients request objects from the Repository using query methods that select objects based on criteria specified by the client, typically the value of certain attributes. The Repository retrieves the requested object, encapsulating the machinery of database queries and metadata mapping. Repositories can implement a variety of queries that select objects based on whatever criteria the client requires. They can also return summary information, such as a count of how many instances meet some criteria. They can even return summary calculations, such as the total across all matching objects of some numerical attribute.

F or each type of object that needs global access, create an object that can provide the illusion of an in-memory collection of all objects of that type. Set up access through a well-k nown global interface. Provide methods to add and remove objects, which will encapsulate the actual insertion or removal of data in the data store. Provide methods that select objects based on some criteria and return fully instantiated objects or collections of objects whose attribute values meet the criteria, thereby encapsulating the actual storage and query technology. Provide Repositories only for Aggregate roots that actually need direct access. Keep the client focused on the model, delegating all object storage and access to the Repositories.

Advantages:

* They present clients with a simple model for obtaining persistent objects and managing their life cycle.
* They decouple application and domain design from persistence technology, multiple database strategies, or even multiple data sources.
* They communicate design decisions about object access.
* They allow easy substitution of a dummy implementation, for use in testing (typically using an inmemory collection).

The easiest Repository to build has hard-coded queries with specific parameters. These queries can be various: retrieving an Entity by its identity (provided by almost all Repositories); requesting a collection of objects with a particular attribute value or a complex combination of parameters; selecting objects based on value ranges (such as date ranges); and even performing some calculations that fall within the general responsibility of a Repository (especially drawing on operations supported by the underlying database).

Implementation will vary greatly, depending on the technology being used for persistence and the infrastructure you have. The ideal is to hide all the inner workings from the client (although not from the developer of the client), so that client code will be the same whether the data is stored in an object database, stored in a relational database, or simply held in memory. The Repository will delegate to the appropriate infrastructure services to get the job done. Encapsulating the mechanisms of storage, retrieval, and query is the most basic feature of a Repository implementation.

* Abstract the type. A Repository “contains” all instances of a specific type, but this does not mean that you need one Repository for each class. The type could be an abstract superclass of a hierarchy. The type could be an interface whose implementers are not even hierarchically related. Or it could be a specific concrete class. Keep in mind that you may well face constraints imposed by the lack of such polymorphism in your database technology.
* Take advantage of the decoupling from the client. You have more freedom to change the implementation of a Repository than you would if the client were calling the mechanisms directly. You can take advantage of this to optimize for performance, by varying the query technique or by caching objects in memory, freely switching persistence strategies at any time. You can facilitate testing of the client code and the domain objects by providing an easily manipulated, dummy in-memory strategy.
* Leave transaction control to the client. Although the Repository will insert into and delete from the database, it will ordinarily not commit anything. It is tempting to commit after saving, for example, but the client presumably has the context to correctly initiate and commit units of work. Transaction management will be simpler if the Repository keeps its hands off.

## Bounded Context

A bounded context delimits the applicability of a particular model so that team members have a clear and shared understanding of what has to be consistent and how it relates to other contexts. Within that context, work to keep the model logically unified, but do not worry about applicability outside those bounds. In other context, other models apply, with differences in terminology, in concepts and rules, and in dialects of the ubiquitous lanuage. By drawing an explicit boundary, you can keep the model pure, and therefore potent, where it is applicable. At the same time, you avoid confusion when shifting your attention to other contexts. Integration across the boundaries necessarily will involve some translation, which you can analyze explicitly.

### Integration patterns

* Partnership: Bounded contexts are integrated in an ad hoc manner.
* Shared kernel: Two or more bounded contexts are integrated by sharing a limited overlapping model that belongs to all participating bounded contexts.
* Conformist: The consumer conforms to the service provider’s model.
* Anticorruption layer: The consumer translates the service provider’s model into a model that fits the consumer’s needs.
* Open-host service: The service provider implements a published language—a model optimized for its consumers’ needs.
* Separate ways: It’s less expensive to duplicate particular functionality than to collaborate and integrate it.

## References

[Domain-Driven Design: Tackling Complexity in the Heart of Software](https://www.amazon.com/-/es/Eric-Evans/dp/0321125215)

[Learning Domain-Driven Design: Aligning Software Architecture and Business Strategy](https://www.amazon.com/Learning-Domain-Driven-Design-Aligning-Architecture/dp/1098100131)
