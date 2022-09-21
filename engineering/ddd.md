# Domain-Driven Design

## Business domain/subdomain

A business domain defines a company’s main area of activity. Generally speaking, it’s the service the company provides to its clients. A company can operate in multiple business domains. It’s important to note that companies may change their business domains often.

To achieve its business domain’s goals and targets, a company has to operate in multiple subdomains. A subdomain is a fine-grained area of business activity. All of a company’s subdomains form its business domain: the service it provides to its customers. Implementing a single subdomain is not enough for a company to succeed; it’s just one building block in the overarching system. The subdomains have to interact with each other to achieve the company’s goals in its business domain.

### Types of subdomain

* Core: A core subdomain is what a company does differently from its competitors. This may involve inventing new products or services or reducing costs by optimizing existing processes.
* Generic: Generic subdomains are business activities that all companies are performing in the same way. Like core subdomains, generic subdomains are generally complex and hard to implement. However, generic subdomains do not provide any competitive edge for the company. There is no need for innovation or optimization here: battletested implementations are widely available, and all companies use them.
* Supporting: As the name suggests, supporting subdomains support the company’s business. However, contrary to core subdomains, supporting subdomains do not provide any competitive advantage. Supporting subdomains are simple. Their business logic resembles mostly data entry screens and ETL (extract, transform, load) operations; that is, the so-called CRUD (create, read, update, and delete) interfaces. These activity areas do not provide any competitive advantage for the company, and therefore do not require high entry barriers.

### Domain expert

Domain experts are subject matter experts who know all the intricacies of the business that we are going to model and implement in code. In other words, domain experts are knowledge authorities in the software’s business domain. The domain experts are neither the analysts gathering the requirements nor the engineers designing the system. Domain experts represent the business. They are the people who identified the business problem in the first place and from whom all business knowledge originates. Systems analysts and engineers are transforming their mental models of the business domain into software requirements and source code.

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

An object defined primarily by its identity is called an Entity. Entities have special modeling and design considerations. They have life cycles that can radically change their form and content, but a thread of continuity must be maintained. Their identities must be defined so that they can be effectively tracked. Their class definitions, responsibilities, attributes, and associations should revolve around who they are, rather than the particular attributes they carry. Even for Entities that don’t transform so radically or have such complicated life cycles, placing them in the semantic category leads to more lucid models and more robust implementations.

When an object is distinguished by its identity, rather than its attributes, make this primary to its definition in the model. Keep the class definition simple and focused on life cycle continuity and identity. Define a means of distinguishing each object regardless of its form or history. Be alert to requirements that call for matching objects by attributes. Define an operation that is guaranteed to produce a unique result for each object, possibly by attaching a symbol that is guaranteed unique. This means of identification may come from the outside, or it may be an arbitrary identifier created by and for the system, but it must correspond to the identity distinctions in the model. The model must define what it means to be the same thing.

It is natural to think about the attributes when modeling an object, and it is quite important to think about its behavior. But the most basic responsibility of Entities is to establish continuity so that behavior can be clear and predictable. They do this best if they are kept spare. Rather than focusing on the attributes or even the behavior, strip the Entity object’s definition down to the most intrinsic characteristics, particularly those that identify it or are commonly used to find or match it. Add only behavior that is essential to the concept and attributes that are required by that behavior. Beyond that, look to remove behavior and attributes into other objects associated with the core Entity.

### Value objects

An object that represents a descriptive aspect of the domain with no conceptual identity is called a Value Object. Value Object are instantiated to represent elements of the design that we care about only for what they are, not who or which they are.

Defining Value Objects and designating them as immutable is a case of following a general rule: Avoiding unnecessary constraints in a model leaves developers free to do purely technical performance tuning. Explicitly defining the essential constraints lets developers tweak the design while keeping safe from changing meaningful behavior. Such design tweaks are often very specific to the technology in use on a particular project.

### Services

A Service is an operation offered as an interface that stands alone in the model, without encapsulating state, as Entities and Value Objects do. Services are a common pattern in technical frameworks, but they can also apply in the domain layer.

The name service emphasizes the relationship with other objects. Unlike Entities and Value Objects, it is defined purely in terms of what it can do for a client. A Service tends to be named for an activity, rather than an entity—a verb rather than a noun. A Service can still have an abstract, intentional definition; it just has a different flavor than the definition of an object. A Service should still have a defined responsibility, and that responsibility and the interface fulfilling it should be defined as part of the domain model. Operation names should come from the Ubiquitous Language or be introduced into it. Parameters and results should be domain objects.

A good Service has three characteristics.

* The operation relates to a domain concept that is not a natural part of an Entity or Value Object.
* The interface is defined in terms of other elements of the domain model.
* The operation is stateless.

Statelessness here means that any client can use any instance of a particular Service without regard to the instance’s individual history. The execution of a Service will use information that is accessible globally, and may even change that global information (that is, it may have side effects). But the Service does not hold state of its own that affects its own behavior, as most domain objects do. When a significant process or transformation in the domain is not a natural responsibility of an Entity or Value Object, add an operation to the model as a standalone interface declared as a Service. Define the interface in terms of the language of the model and mak e sure the operation name is part of the Ubiquitous Language. Make the Service stateless.

### Aggregates

An Aggregate is a cluster of associated objects that we treat as a unit for the purpose of data changes. Each Aggregate has a root and a boundary. The boundary defines what is inside the Aggregate. The root is a single, specific Entity contained in the Aggregate. The root is the only member of the Aggregate that outside objects are allowed to hold references to, although objects within the boundary may hold references to each other. Entities other than the root have local identity, but that identity needs to be distinguishable only within the Aggregate, because no outside object can ever see it out of the context of the root Entity.

Invariants, which are consistency rules that must be maintained whenever data changes, will involve relationships between members of the Aggregate. Any rule that spans Aggregates will not be expected to be up-to-date at all times. Through event processing, batch processing, or other update mechanisms, other dependencies can be resolved within some specified time. But the invariants applied within an Aggregate will be enforced with the completion of each transaction.

Rules to implement Aggregates:

* The root Entity has global identity and is ultimately responsible for checking invariants.
* Root Entities have global identity. Entities inside the boundary have local identity, unique only within the Aggregate.
* Nothing outside the Aggregate boundary can hold a reference to anything inside, except to the root Entity. The root Entity can hand references to the internal Entities to other objects, but those objects can use them only transiently, and they may not hold on to the reference. The root may hand a copy of a Value Object to another object, and it doesn’t matter what happens to it, because it’s just a Value and no longer will have any association with the Aggregate.
* As a corollary to the previous rule, only Aggregate roots can be obtained directly with database queries. All other objects must be found by traversal of associations.
* Objects within the Aggregate can hold references to other Aggregate roots.
* A delete operation must remove everything within the Aggregate boundary at once. (With garbage collection, this is easy. Because there are no outside references to anything but the root, delete the root and everything else will be collected.)
* When a change to any object within the Aggregate boundary is committed, all invariants of the whole Aggregate must be satisfied.

Cluster the Entities and Value Objects into Aggregates and define boundaries around each. Choose one Entity to be the root of each Aggregate, and control all access to the objects inside the boundary through the root. Allow external objects to hold references to the root only. Transient references to internal members can be passed out for use within a single operation only. Because the root controls access, it cannot be blindsided by changes to the internals. This arrangement makes it practical to enforce all invariants for objects in the Aggregate and for the Aggregate as a whole in any state change.

### Factory

A program element whose responsibility is the creation of other objects is called a Factory. Just as the interface of an object should encapsulate its implementation, thus allowing a client to use the object’s behavior without knowing how it works, a Factory encapsulates the knowledge needed to create a complex object or Aggregate. It provides an interface that reflects the goals of the client and an abstract view of the created object.

Shift the responsibility for creating instances of complex objects and Aggregates to a separate object, which may itself have no responsibility in the domain model but is still part of the domain design. Provide an interface that encapsulates all complex assembly and that does not require the client to reference the concrete classes of the objects being instantiated. Create entire Aggregates as a piece, enforcing their invariants.

Basic requirements for a factory:

* Each creation method is atomic and enforces all invariants of the created object or Aggregate. A Factory should only be able to produce an object in a consistent state. For an Entity, this means the creation of the entire Aggregate, with all invariants satisfied, but probably with optional elements still to be added. For an immutable Value Object, this means that all attributes are initialized to their correct final state. If the interface makes it possible to request an object that can’t be created correctly, then an exception should be raised or some other mechanism should be invoked that will ensure that no improper return value is possible.
* The Factory should be abstracted to the type desired, rather than the concrete class(es) created.

A Factory is very tightly coupled to its product, so a Factory should be attached only to an object that has a close natural relationship with the product. When there is something we want to hide—either the concrete implementation or the sheer complexity of construction—yet there doesn’t seem to be a natural host, we must create a dedicated Factory object or Service. A standalone Factory usually produces an entire Aggregate, handing out a reference to the root, and ensuring that the product Aggregate's invariants are enforced. If an object interior to an Aggregate needs a Factory, and the Aggregate root is not a reasonable home for it, then go ahead and make a standalone Factory. But respect the rules limiting access within an Aggregate, and make sure there are only transient references to the product from outside the Aggregate.

### Repository

A Repository represents all objects of a certain type as a conceptual set (usually emulated). It acts like a collection, except with more elaborate querying capability. Objects of the appropriate type are added and removed, and the machinery behind the Repository inserts them or deletes them from the database. This definition gathers a cohesive set of responsibilities for providing access to the roots of Aggregates from early life cycle through the end.

Clients request objects from the Repository using query methods that select objects based on criteria specified by the client, typically the value of certain attributes. The Repository retrieves the requested object, encapsulating the machinery of database queries and metadata mapping. Repositories can implement a variety of queries that select objects based on whatever criteria the client requires. They can also return summary information, such as a count of how many instances meet some criteria. They can even return summary calculations, such as the total across all matching objects of some numerical attribute.

For each type of object that needs global access, create an object that can provide the illusion of an in-memory collection of all objects of that type. Set up access through a well-known global interface. Provide methods to add and remove objects, which will encapsulate the actual insertion or removal of data in the data store. Provide methods that select objects based on some criteria and return fully instantiated objects or collections of objects whose attribute values meet the criteria, thereby encapsulating the actual storage and query technology. Provide Repositories only for Aggregate roots that actually need direct access. Keep the client focused on the model, delegating all object storage and access to the Repositories.

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

## Supple design

Supple design is the complement to deep modeling. Once you’ve dug out implicit concepts and made them explicit, you have the raw material. Through the iterative cycle, you hammer that material into a useful shape, cultivating a model that simply and clearly captures the key concerns, and shaping a design that allows a client developer to really put that model to work. Development of the design and code leads to insight that refines model concepts.

### Intention-Revealing Interfaces

If a developer must consider the implementation of a component in order to use it, the value of encapsulation is lost. If someone other than the original developer must infer the purpose of an object or operation based on its implementation, that new developer may infer a purpose that the operation or class fulfills only by chance. If that was not the intent, the code may work for the moment, but the conceptual basis of the design will have been corrupted, and the two developers will be working at cross-purposes.

Name classes and operations to describe their effect and purpose, without reference to the means by which they do what they promise. This relieves the client developer of the need to understand the internals. These names should conform to the Ubiquitous Language so that team members can quickly infer their meaning. Write a test for a behavior before creating it, to force your think ing into client developer mode.

### Side-Effect-Free functions

Interactions of multiple rules or compositions of calculations become extremely difficult to predict. The developer calling an operation must understand its implementation and the implementation of all its delegations in order to anticipate the result. The usefulness of any abstraction of interfaces is limited if the developers are forced to pierce the veil. Without safely predictable abstractions, the developers must limit the combinatory explosion, placing a low ceiling on the richness of behavior that is feasible to build.

Place as much of the logic of the program as possible into functions, operations that return results with no observable side effects. Strictly segregate commands (methods that result in modifications to observable state) into very simple operations that do not return domain information. Further control side effects by moving complex logic into Value Objects when a concept fitting the responsibility presents itself.

### Assertions

When the side effects of operations are only defined implicitly by their implementation, designs with a lot of delegation become a tangle of cause and effect. The only way to understand a program is to trace execution through branching paths. The value of encapsulation is lost. The necessity of tracing concrete execution defeats abstraction.

State post-conditions of operations and invariants of classes and Aggregates. If Assertions cannot be coded directly in your programming language, write automated unit tests for them. Write them into documentation or diagrams where it fits the style of the project’s development process. Seek models with coherent sets of concepts, which lead a developer to infer the intended Assertions, accelerating the learning curve and reducing the risk of contradictory code.

### Conceptual contours

When elements of a model or design are embedded in a monolithic construct, their functionality gets duplicated. The external interface doesn’t say everything a client might care about. Their meaning is hard to understand, because different concepts are mixed together. On the other hand, breaking down classes and methods can pointlessly complicate the client, forcing client objects to understand how tiny pieces fit together. Worse, a concept can be lost completely. Half of a uranium atom is not uranium. And of course, it isn’t just grain size that counts, but just where the grain runs.

Decompose design elements (operations, interfaces, classes, and Aggregates) into cohesive units, taking into consideration your intuition of the important divisions in the domain. Observe the axes of change and stability through successive refactorings and look for the underlying Conceptual Contours that explain these shearing patterns. Align the model with the consistent aspects of the domain that make it a viable area of knowledge in the first place.

### Standalone Classes

Even within a Module, the difficulty of interpreting a design increases wildly as dependencies are added. This adds to mental overload, limiting the design complexity a developer can handle. Implicit concepts contribute to this load even more than explicit references. Try to factor the most intricate computations into Standalone Classess, perhaps by modeling Value Objects held by the more connected classes. Low coupling is a basic way to reduce conceptual overload. A Standalone Class is an extreme example of low coupling.

### Closure of Operations

Where it fits, define an operation whose return type is the same as the type of its argument(s). If the implementer has state that is used in the computation, then the implementer is effectively an argument of the operation, so the argument(s) and return value should be of the same type as the implementer. Such an operation is closed under the set of instances of that type. A closed operation provides a high-level interface without introducing any dependency on other concepts.

## Bounded Context

A Bounded Context delimits the applicability of a particular model so that team members have a clear and shared understanding of what has to be consistent and how it relates to other contexts. Within that context, work to keep the model logically unified, but do not worry about applicability outside those bounds. In other context, other models apply, with differences in terminology, in concepts and rules, and in dialects of the ubiquitous lanuage. By drawing an explicit boundary, you can keep the model pure, and therefore potent, where it is applicable. At the same time, you avoid confusion when shifting your attention to other contexts. Integration across the boundaries necessarily will involve some translation, which you can analyze explicitly.

Combining elements of distinct models causes two categories of problems

* Duplication of concepts: There are two model elements (and attendant implementations) that actually represent the same concept. Every time this information changes, it has to be updated in two places with conversions. Every time new knowledge leads to a change in one of the objects, the other has to be reanalyzed and changed too. Except the reanalysis doesn’t happen in reality, so the result is two versions of the same concept that follow different rules and even have different data. On top of that, the team members must learn not one but two ways of doing the same thing, along with all the ways they are being synchronized.
* False cognates: This is the case when two people who are using the same term (or implemented object) think they are talking about the same thing, but really are not. False cognates lead to development teams that step on each other’s code, databases that have weird contradictions, and confusion in communication within the team.

### Continuous integration

Continuous Integration means that all work within the context is being merged and made consistent frequently enough that when splinters happen they are caught and corrected quickly. Continuous Integration, like everything else in domain-driven design, operates at two levels: (1) the integration of model concepts and (2) the integration of the implementation. Concepts are integrated by constant communication among team members. The team must cultivate a shared understanding of the ever-changing model. Many practices help, but the most fundamental is constantly hammering out the Ubiquitous Language. Meanwhile, the implementation artifacts are being integrated by a systematic merge/build/test process that exposes model splinters early.

### Context Map

A Context Map is in the overlap between project management and software design. The natural course of events is for the boundaries to follow the contours of team organization. People who work closely will naturally share a model context. People on different teams, or those that don’t talk, even if they are on the same team, will split off into different contexts. Physical office space can have an impact too, as team members on opposite ends of a building—not to mention different cities—will probably diverge without extra integration effort. Most project managers intuitively recognize these factors and broadly organize teams around subsystems. But the interrelationship between team organization and software model and design is still not prominent enough. Both managers and team members need a clear view into the ongoing conceptual subdivision of the software model and design.

### Integration patterns

* Partnership: Bounded Contexts are integrated in an ad hoc manner.
* Shared Kernel: Two or more Bounded Contexts are integrated by sharing a limited overlapping model that belongs to all participating Bounded Contexts.
* Conformist: The consumer conforms to the service provider’s model.
* Anticorruption layer: The consumer translates the service provider’s model into a model that fits the consumer’s needs.
* Open-host service: The service provider implements a published language—a model optimized for its consumers’ needs.
* Separate ways: It’s less expensive to duplicate particular functionality than to collaborate and integrate it.

## Large-scale structure

A “large-scale structure” is a language that lets you discuss and understand the system in broad
strokes. A set of high-level concepts or rules, or both, establishes a pattern of design for an entire system. This organizing principle can guide design as well as aid understanding. It helps coordinate independent work because there is a shared concept of the big picture: how the roles of various parts shape the whole. Devise a pattern of rules or roles and relationships that will span the entire system and that allows some understanding of each part’s place in the whole— even without detailed knowledge of the part’s responsibility.

Structure may be confined to one Bounded Context but will usually span more than one, providing the
conceptual organization to hold together all the teams and subsystems involved in the project. A good structure gives insight into the model and complements distillation. You can’t represent most large-scale structures in UML, and you don’t need to. Most large-scale structures shape and explain the model and design but do not appear in it. They provide an extra level of communication about the design.

### Envolving order

An up-front imposition of a large-scale structure is likely to be costly. As development proceeds, you will almost certainly find a more suitable structure, and you may even find that the prescribed structure is prohibiting you from taking a design route that would greatly clarify or simplify the application. You may be able to use some of the structure, but you’re forgoing opportunities. Your work slows down as you try workarounds or try to negotiate with the architects. But your managers think the architecture is done. It was supposed to make this application easy, so why aren’t you working on the application instead of dealing with all these architecture problems? The managers and architecture teams may even be open to input, but if each change is a heroic battle, it is too exhausting.

Design free-for-alls produce systems no one can mak e sense of as a whole, and they are
very difficult to maintain. But architectures can straitjack et a project with up-front
design assumptions and tak e too much power away from the developers/designers of
particular parts of the application. Soon, developers will dumb down the application to
fit the structure, or they will subvert it and have no structure at all, bringing back the
problems of uncoordinated development.

The problem is not the existence of guiding rules, but rather the rigidity and source of those rules. If the rules governing the design really fit the circumstances, they will not get in the way but actually push development in a helpful direction, as well as provide consistency. Let this conceptual large-scale structure evolve with the application, possibly changing to a completely different type of structure along the way. Don’t overconstrain the detailed design and model decisions that must be made with detailed k nowledge.

Large-scale structure should be applied when a structure can be found that greatly clarifies the system without forcing unnatural constraints on model development. Because an ill-fitting structure is worse than none, it is best not to shoot for comprehensiveness, but rather to find a minimal set that solves the problems that have emerged. Less is more. A large-scale structure can be very helpful and still have a few exceptions, but those exceptions need to be flagged somehow, so that developers can assume the structure is being followed unless otherwise noted. And if
those exceptions start to get numerous, the structure needs to be changed or discarded.

### System Metaphor

Software designs tend to be very abstract and hard to grasp. Developers and users alike need tangible ways to understand the system and share a view of the system as a whole. On one level, metaphor runs so deeply in the way we think that it pervades every design. Systems have “layers” that “lay on top” of each other. They have “kernels” at their “centers.” But sometimes a metaphor comes along that can convey the central theme of a whole design and provide a shared understanding among all team members. When this happens, the system is actually shaped by the metaphor. A developer will make design decisions consistent with the System Metaphor. This consistency will enable other developers to interpret the many parts of a complex system in terms of the same metaphor. The developers and experts have a reference point in discussions that may be more concrete than the model itself.

A System Metaphor is a loose, easily understood, large-scale structure that it is harmonious with the object paradigm. Because the System Metaphor is only an analogy to the domain anyway, different models can map to it in an approximate way, which allows it to be applied in multiple Bounded Contexts, helping to coordinate work between them.

When a concrete analogy to the system emerges that captures the imagination of team members and seems to lead think ing in a useful direction, adopt it as a large-scale structure. Organize the design around this metaphor and absorb it into the Ubiquitous Language. The System Metaphor should both facilitate communication about the system and guide development of it. This increases consistency in different parts of the system, potentially even across different Bounded Contexts. But because all metaphors are inexact, continually reexamine the metaphor for overextension or
inaptness, and be ready to drop it if it gets in the way.

### Responsability layers

When each individual object has handcrafted responsibilities, there are no guidelines, no uniformity, and no ability to handle large swaths of the domain together. To give coherence to a large model, it is useful to impose some structure on the assignment of those responsibilities.

Look at the conceptual dependencies in your model and the varying rates and sources of change of different parts of your domain. If you identify natural strata in the domain, cast them as broad abstract responsibilities. These responsibilities should tell a story of the high-level purpose and design of your system. Refactor the model so that the responsibilities of each domain object, Aggregate, and Module fit neatly within the responsibility of one layer.

### Pluggable component framework

When a variety of applications have to interoperate, all based on the same abstractions but designed independently, translations between multiple Bounded Contexts limit integration. A Shared Kernel is not feasible for teams that do not work closely together. Duplication and fragmentation raise costs of development and installation, and interoperability becomes very difficult.

Distill an Abstract Core of interfaces and interactions and create a framework that allows diverse implementations of those interfaces to be freely substituted. Lik ewise, allow any application to use those components, so long as it operates strictly through the interfaces of the Abstract Core. High-level abstractions are identified and shared across the breadth of the system; specialization occurs in Modules. The central hub of the application is an Abstract Core within a Shared Kernel. But multiple Bounded Contexts can lie behind the encapsulated component interfaces, so that this structure can be especially convenient when many components are coming from many different sources, or when components are encapsulating preexisting software for integration.

## Essentials for Startegic Design Decision Making

### Decisions must reach the entire team

Obviously, if everyone doesn’t know the strategy and follow it, it is irrelevant. This requirement leads people to organize around centralized architecture teams with official “authority”—so that the same rules will be applied everywhere. Ironically, ivory tower architects are often ignored or bypassed. Developers have no choice when the architects’ lack of feedback from hands-on attempts to apply their own rules to real applications results in impractical schemes. On a project with very good communication, a strategic design that emerges from the application team may actually reach everyone more effectively. The strategy will be relevant, and it will have the authority that attaches to intelligent community decisions. Whatever the system, be less concerned with the authority bestowed by management than with the actual relationship the developers have with the strategy.

### The decision process must absorb feecback

Creating an organizing principle, large-scale structure, or distillation of such subtlety requires a really deep understanding of the needs of the project and the concepts of the domain. The only people who have that depth of knowledge are the members of the application development team. This explains why application architectures created by architecture teams are so seldom helpful, despite the undeniable talent of many of the architects. Unlike technical infrastructure and architectures, strategic design does not itself involve writing a lot of code, although it influences all development. What it does require is involvement with the application development teams. An experienced architect may be able to listen to ideas coming from various teams and facilitate the development of a generalized solution.

### The plan must allow for evolution

Effective software development is a highly dynamic process. When the highest level of decisions is set in stone, the team has fewer options when it must respond to change. Envolving order avoids this trap by emphasizing ongoing change to the large-scale structure in response to deepening insight. When too many design decisions are preordained, the development team can be hobbled, without the flexibility to solve the problems they are charged with. So, while a harmonizing principle can be valuable, it must grow and change with the ongoing life of the development project, and it must not take too much power away from the application developers, whose job is hard enough as it is. With strong feedback, innovations emerge as obstacles are encountered in building applications and as unexpected opportunities are discovered.

### Architecture teams must not siphon off all the best and brightest

Design at this level calls for sophistication that is probably in short supply. Managers tend to move the most technically talented developers into architecture teams and infrastructure teams, because they want to leverage the skills of these advanced designers. For their part, the developers are attracted to the opportunity to have a broader impact or to work on “more interesting” problems. And there is prestige attached to being a member of an elite team.

Conversely, such teams almost never include the developer who perhaps has weaker design skills but who has the most extensive experience in the domain. Strategic design is not a purely technical task; cutting themselves off from developers with deep domain knowledge hobbles the architects’ efforts further. And domain experts are needed too. It is essential to have strong designers on all application teams. It is essential to have domain knowledge on any team attempting strategic design. It may simply be necessary to hire more advanced designers. It may help to keep architecture teams part-time.

### Strategic design requires minimalism and humility

Distillation and minimalism are essential to any good design work, but minimalism is even more critical for strategic design. Even the slightest ill fit has a terrible potential for getting in the way. Separate architecture teams have to be especially careful because they have less feel for the obstacles they might be placing in front of application teams. At the same time, the architects’ enthusiasm for their primary responsibility makes them more likely to get carried away.

Instead, we have to discipline ourselves to produce organizing principles and core models that are pared down to contain nothing that does not significantly improve the clarity of the design. The truth is, almost everything gets in the way of something, so each element had better be worth it. Realizing that your best idea is likely to get in somebody’s way takes humility.

### Objects are specialists; developers are generalists

The essence of good object design is to give each object a clear and narrow responsibility and to reduce interdependence to an absolute minimum. Sometimes we try to make interactions on teams as tidy as they should be in our software. A good project has lots of people sticking their nose in other people’s business. Developers play with frameworks. Architects write application code. Everyone talks to everyone. It is efficiently chaotic. Make the objects into specialists; let the developers be generalists.

Creating a supple design based on a deep model is an advanced design activity, but the details are so important that it has to be done by someone working with the code. Strategic design emerges out of application design, yet it requires a big-picture view of activity, possibly spanning multiple teams. People love to find ways to chop up tasks so that design experts don’t have to know the business and domain experts don’t have to understand technology. There is a limit to how much an individual can learn, but overspecialization takes the steam out of domain-driven design.

## References

[Domain-Driven Design: Tackling Complexity in the Heart of Software](https://www.amazon.com/-/es/Eric-Evans/dp/0321125215)

[Learning Domain-Driven Design: Aligning Software Architecture and Business Strategy](https://www.amazon.com/Learning-Domain-Driven-Design-Aligning-Architecture/dp/1098100131)
