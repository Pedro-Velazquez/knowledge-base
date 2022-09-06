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

## Bounded Context

A bounded context delimits the applicability of a particular model so that team members have a clear and shared understanding of what has to be consistent and how it relates to other contexts. Within that context, work to keep the model logically unified, but do not worry about applicability outside those bounds. In other context, other models apply, with differences in terminology, in concepts and rules, and in dialects of the ubiquitous lanuage. By drawing an explicit boundary, you can keep the model pure, and therefore potent, where it is applicable. At the same time, you avoid confusion when shifting your attention to other contexts. Integration across the boundaries necessarily will involve some translation, which you can analyze explicitly.

### Integration patterns

* Partnership: Bounded contexts are integrated in an ad hoc manner.
* Shared kernel: Two or more bounded contexts are integrated by sharing a limited overlapping model that belongs to all participating bounded contexts.
* Conformist: The consumer conforms to the service provider’s model.
* Anticorruption layer: The consumer translates the service provider’s model into a model that fits the consumer’s needs.
* Open-host service: The service provider implements a published language—a model optimized for its consumers’ needs.
* Separate ways: It’s less expensive to duplicate particular functionality than to collaborate and integrate it.
