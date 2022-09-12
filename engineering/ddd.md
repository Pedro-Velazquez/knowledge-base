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
