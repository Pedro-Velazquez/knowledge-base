# Microservices

## Advantages
* Enable continuous delivery.
* Allow for an efficient developer workflow because they’re highly maintainable.
* Are robust by design.
* Can scale up or down independently of each other.

## Key characteristics
* A microservice is responsible for a single capability.
* A microservice is individually deployable.
* A microservice consists of one or more processes.
* A microservice owns its own data store.
* A small team can maintain a few handfuls of microservices.
* A microservice is replaceable.

## Microservices architecture style
Microservices as an architectural
style is a lightweight form of service-oriented architecture (SOA) where the
services are each tightly focused on doing one thing and doing it well. A system with a
microservices architecture is a distributed system with a (probably large) number of
collaborating microservices.
The microservices architectural style has been quickly gaining in popularity for
building and maintaining complex server-side software systems. And understandably
so: microservices offer a number of potential benefits over both more traditional
service-oriented approaches and monolithic architectures. Microservices, when done
well, are malleable, scalable, and robust.

## Scoping microservices
To succeed with microservices, it’s important to be good at scoping each microservice
appropriately. If your microservices are too big, the turnaround on creating
new features and implementing bug fixes becomes longer than it needs to. If
they’re too small, the coupling between microservices tends to grow. If they’re the
right size but have the wrong boundaries, coupling also tends to grow, and higher
coupling also leads to longer turnaround. In other words, if you aren’t able to
scope your microservices correctly, you’ll lose much of the benefit microservices
offer. The main drivers to identifying and scoping microservices are:
* Business capabilities.
* Supporting technical capabilities.
* Supporting efficiency of work.
### Business capability
A business capability is something an organization does that contributes to business goals. A given business will have a number of business capabilities that together make the overall business function.
When mapping a business capability to a microservice, the microservice models the
business capability. In some cases, the microservice implements the entire business
capability and automates it completely. In other cases, the microservice implements
only part of the business capability, because some part of the capability is carried out by people in the real world and thus the microservice only partly automates the business capability. In both cases, the scope of the microservice is the business capability.

A good understanding of the domain will enable you to understand how the business
functions. Understanding how the business functions means you can identify the business
capabilities that make up the business and the processes involved in delivering the
capabilities. In other words, the way to identify business capabilities is to learn about the
business’s domain. You can gain this type of knowledge by talking with the people who
know the business domain best: business analysts, the end users of your software, and so
on—all the people directly involved in the day-to-day work that drives the business.

A business’s organization usually reflects its domain. Different parts of the domain
are handled by different groups of people, and each group is responsible for delivering
certain business capabilities; so, this organization can give you hints about how the
microservices should be scoped. For one thing, a microservice’s responsibility should
probably lie within the purview of only one group. If it crosses the boundary between
two groups, it’s probably too widely scoped and will be difficult to keep cohesive, leading
to low maintainability.

### Supporting technical capability
A supporting technical capability is something that doesn’t directly contribute
to a business goal but supports other microservices, such as integrating with
another system or scheduling an event to happen some time in the future. Supporting technical capabilities are secondary drivers in scoping microservices because they don’t directly contribute to the system’s business goals. They exist to simplify and support the other microservices that implement business capabilities. One characteristic of a good microservice is that it’s replaceable; but if a microservice that implements a business capability also implements a complex technical capability, it may grow too large and too complex to be replaceable. In such cases, you should consider implementing the technical capability in a separate microservice
that supports the original one.

When you introduce supporting technical microservices, your goal is to simplify the
microservices that implement business capabilities. Sometimes—such as with sending
notifications—you identify a set of technical capabilities that several microservices
need, and you turn that into a bounded context with microservices of its own, so
other microservices can share the implementation. Other times—as with the ERP
integration—you identify a technical capability that unduly complicates a microservice
and turn that capability into a microservice of its own. In both cases, the other
microservices implementing business capabilities are left with one less technical concern
to take care of.

When deciding to implement a technical capability in a separate microservice, be
careful that you don’t violate the microservice characteristic of being individually
deployable. It makes sense to implement a technical capability in a separate microservice
only if that microservice can be deployed and redeployed independently of
any other microservices. Likewise, deploying the microservices that are supported by
the microservice providing the technical capability must not force you to redeploy the
microservice implementing the technical capability.

Identifying business capabilities and microservices based on business capabilities is
a strategic exercise, but identifying technical supporting capabilities that could be
implemented by separate microservices is an opportunistic exercise. The question of
whether a supporting technical capability should be implemented in its own microservice
is about what will be easiest in the long run.

### Supporting efficiency fof work
The microservices we design and create should be efficient to
work with and should let teams that develop and maintain the microservices work efficiently. If we have an already defined organization that we cannot change, the system of
microservices we create must align with the organization. On the other hand, if the
organization can be changed we should do so in accordance with the overall system of
microservices. This, largely, is a matter of respecting and using Conway’s law:

<i>"Any organization that designs a system (defined broadly) will produce a design whose
structure is a copy of the organization’s communication structure."</i>

First and foremost, respecting Conway’s law means we should make sure that there
is a clear ownership of each microservice: we should assign one team to the development
and maintenance of each microservice. This is in line with the microservices
characteristic that a small team can maintain a few handfuls of microservices. Each
can be be assigned a few handfuls of services to be responsible for. It is important that
the responsibility is clear. If the responsibility for a microservice is split between two or
more teams, we introduce a need for those teams to coordinate closely whenever
changes to that microservices need to happen. That coordination takes time and
means that none of the teams involved can work autonomously. This is a form of inefficiency,
and it is something we can avoid if we make sure each microservices is
assigned to one team.

## Factors that make it difficult to identify scopes
* Insufficient understanding of the business domain.
* Confusion in the business domain.
* Incomplete knowledge of the details of a technical capability.
* Inability to estimate the complexity of a technical capability.

## Microservices collaboration
Each microservice implements a single capability, but to deliver end-user functionality,
microservices need to collaborate. Microservices can use three main communication
styles for collaboration: commands, queries, and events. Each style has its
strengths and weaknesses, and understanding the tradeoffs between them allows
you to pick the appropriate one for each microservice collaboration. When you get
the collaboration style right, you can implement loosely coupled microservices with
clear boundaries.
* Commands: Used when one microservice needs another microservice
to perform an action.
* Queries: Used when one microservice needs information from another microservice.
* Events: Used when a microservice needs to react to something that happened in another microservice

Collaboration based on commands and queries should use relatively coarse-grained
commands and queries. The calls made between microservices are remote calls,
meaning they cross at least a process boundary and usually also a network. This means
calls between microservices are relatively slow. Even though the microservices are finegrained,
you must not fall into the trap of thinking of calls from one microservice to
another as being like function calls in a microservice.

Furthermore, you should prefer collaboration based on events over collaboration
based on commands or queries. Event-based collaboration is more loosely coupled
than the other two forms of collaboration because events are handled asynchronously.
That means two microservices collaborating through events aren’t temporally coupled;
the handling of an event doesn’t have to happen immediately after the event is
raised. Rather, handling can happen when the subscriber is ready to do so. In contrast,
commands and queries are synchronous and therefore need to be handled
immediately after they’re sent.

## Failures and errors
When working with any nontrivial software system, you must expect failures to occur.
Hardware can fail. Software may fail due to, for instance, unforeseen usage or corrupt
data. A distinguishing factor of a microservice system is that there’s a lot of communication
between microservices. You must expect communication to fail from time to time.
Communication between two microservices may not fail often, but looking at a microservice
system as a whole, communication failures are likely to occur often due to the
amount of communication.

Because you have to expect that some of the communication in your microservice
system will fail, you should design your microservices to be able to cope with those failures. When a communication fails, the impact depends on the type of collaboration and the way the
microservices cope with it:
* Query-based collaboration: When a query fails, the caller doesn’t get the information
it needs. If the caller copes well with that, the system keeps working, but
with degraded functionality. If the caller doesn’t cope well, the result could be
an error.
* Command-based collaboration: When sending a command fails, the sender can’t
know whether the receiver got the command. Again, depending on how the
sender copes, this could result in an error, or it could result in degraded
functionality.
* Event-based collaboration: When a subscriber polls an event feed but the call
fails, the impact is limited. The subscriber will poll the event feed again later
and, assuming the event feed is up again, receive the events at that time. In
other words, the subscriber will still get all events, but some of them will be
delayed. This shouldn’t be a problem for an event-based collaboration because
it’s asynchronous anyway.

### Tips to handle failures
* Keeping good logs.
* Using tace IDs.
* Don't propagate failures

## Patterns for building applications over microservices

### Composite applications. Integrating at the frontend
A composite application is made up of functionality drawn from several places—
in the case of microservices, from different microservices—by communicating with
each one directly. In this pattern, each microservice provides both functionality and a
UI for the functionality. Microservices may communicate with each other to perform
their tasks; the composite application doesn’t care.

When you’re building composite applications, the UI is split into smaller parts according
to business capabilities, just as functionality is distributed across microservices
following business capabilities. That means the UI for each business capability is implemented close to the code for the capability and is deployed along with that code.
Because the composite application draws the UI for the capability from the microservice,
the application is updated every time a microservice UI is updated. This means
the agility you gain by splitting the system into small, focused microservices applies to
the application UI, too.

A composite application is responsible for integrating all the functionality implemented
throughout the system of microservices. This can be a complex task: there are
potentially many business capabilities in a microservice system, and the application’s
UI may not be split along quite the same lines, leading to pages or screens that
include UIs from several different microservices but that need to feel like a single
screen to the end user.
This kind of complexity can mean that the composite application has intimate
knowledge of how the microservices work and, in particular, how their UIs work. If the
composite application begins to make too many assumptions about the microservices’
UIs, it becomes sensitive to changes in each microservice, and thus the application as
a whole may break because of GUI changes in a single microservice. If you wind up in
that situation, you lose the agility that’s one of the major advantages of using a composite
application.

### API Gateway
An API Gateway is a microservice with a public HTTP API that covers all the system’s
functionality but doesn’t implement any of the functionality itself. Instead, the API Gateway
delegates everything to other microservices. In effect, an API Gateway acts like an
adapter between applications and the system of microservices. When you build applications in front of a microservice system that uses an API Gateway, the applications are shielded from knowing anything about how the system functionality is split across microservices, or even that the system uses microservices. The application only needs to know about one microservice: the API Gateway.

The main benefit of the API Gateway pattern is that it decouples applications nicely
from the way the system is decomposed into microservices and hides that completely
from applications. In cases where several applications have overlapping functionality
or where some applications are built by third parties, using the API Gateway pattern
facilitates the following:
* Maintaining a low barrier to entry for building applications.
* Keeping the public API stable.
* Keeping the public API backward compatible.

The main disadvantage of the API Gateway pattern is that the API Gateway itself can
grow into a large codebase and display all the disadvantages of a monolith. This is
especially true if you succumb to the temptation to implement business logic in the
API Gateway, which may draw on many other microservices to serve a single request.
Because it’s combining the data from several microservices anyway, it’s tempting to
apply a few business rules to the data as well. Doing so may be quick in the short run,
but it pushes the API Gateway down the path toward becoming a monolith.

### Backend for frontend (BBF) pattern
The BFF pattern is relevant when you need
to build more than one application for a microservice system—for instance, the insurance
system may have a web application for the most common functionality, an iOS
app that appraisers can use on the road, and a specialized desktop application for
actuarial tasks. A BFF is a microservice akin to an API Gateway, but it’s specialized for
one application. If you use this pattern for the applications in the insurance system,
you’ll have a BFF for the web app, a BFF for the iOS app, and a BFF for the actuarial
desktop application.

With the BFF pattern, each application gets to use an API that’s tailored exactly to its
needs. With an API Gateway, there’s a risk of it becoming bloated as you add more and
more functionality to it over time. With a BFF, this is less of a risk, because the BFF
doesn’t have to cover everything in the system, only the functionality needed by the
application it serves.

It’s fairly easy to know when something can be removed from a BFF: when no
active version of the application it serves uses that functionality. Compare this to an
API Gateway with several applications in front: something can be removed from the
API Gateway only when no version of any of the applications uses it. All in all, BFFs
offer a way to both simplify application development and keep the server-side focused
and well factored.

In cases where you have several applications that provide similar or overlapping functionality
to end users—such as having both an iOS app and an Android app targeted
at the same type of end user—the BFF pattern leads to duplicating code among several
BFFs. This comes with the usual disadvantages of duplication: duplicated effort
every time there are changes to the duplicated parts, and a tendency for the duplicated
parts to drift away from each other over time and end up working slightly differently
in different applications.

### When to use each pattern
* How much intelligence do you want to put into the application? For a line-of-business application that’s only used within the company firewall and only on company machines, you may opt to build a desktop application with a lot of intelligence. In that case, the composite application pattern is the obvious choice. For a public-facing e-commerce application meant to run in any browser, with the risk of somebody trying to hack the app, you may shy away from putting
intelligence into the application, making the composite application pattern less attractive.
* Is there more than one application? If so, how different are the applications? If you haven’t put much intelligence in the application, and if there’s only one application, or if all applications provide similar functionality—maybe even in similar ways—an API Gateway is probably a good choice. If there are several applications, and they provide different sets of functionality,
the BFF pattern is a good option. With an API Gateway or with BFFs, the
intelligence is on the backend. The API Gateway works well as long as it’s
cohesive—that is, as long as the set of all endpoints exposed by the API Gateway
has a certain consistency in terms of how applications should use them and how
they’re structured. If some endpoints follow a remote procedure call (RPC) style and others follow
a representation state transfer (REST) style, they’re inconsistent, and cohesion
in the API Gateway codebase will probably be low. In such cases, you should
consider the BFF pattern. With BFFs, you can have some applications that work
with an RPC-style API in one BFF and other apps that use a REST API in another,
without compromising cohesion. Each BFF can be cohesive and consistent by
itself, but you don’t need consistency among BFFs in terms of API style.
* How big is the system? With a large system—in terms of the amount of functionality it exposes—an
API Gateway can become an unmanageable codebase that exposes many of the
disadvantages of monoliths. With large systems, using a number of BFFs is probably
a better choice than one big API Gateway. On the other hand, if the system
isn’t that big, an API Gateway can be simpler than BFFs.

## Resources
* [Microservices in .NET 2nd edition](https://www.amazon.es/Microservices-NET-Core-Christian-Gammelgaard/dp/1617297925)
