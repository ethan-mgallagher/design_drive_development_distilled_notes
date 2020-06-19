# **Summary of Domain Driven Design Distilled**

**Ethan Gallagher**

**06.19.2020**

<br>

<br>

## **Chapter 1**



- Domain Driven Design is a set of tools which help the developer to deliver high-quality software. These tools are useful at both the strategic and tactical levels. By strategic we here mean that DDD can help a product team identify core business competencies and make software design decisions that result in the most competitive advantage for a business. Tactical design is a question of making design choices that help a team deliver on their strategic design.
-   Knowledge acquisition is the process of transferring knowledge from Domain Experts into the design of a software system. In Agile, this involves high-level feature requirements being transformed into stories for the implementation of a software system that meets said requirements.

- Software development is often seen as a cost pit by management, and so there is considerable pressure from management to try and squeeze as much juice out of a product team as possible. In some cases this results in the design phase of projects being shortened or eliminated. However, design is inevitable --- even if a project is not designed properly before coding starts, it will end up having a design at the end. The difference will be that an ad-hoc design will be piecemeal, incoherent, and almost certainly bad. What we want is a well-functioning and effective design.
- Effective design meets the needs of the business organization to the extent that it can distinguish itself from competition by means of software. In order to conduct effective design, the organization must understand what its core competencies are, or what distinguishes it from competitors. Only then can a good software model be devised.

<br>

<br>

## **Chapter 2 - Strategic Design with Bounded Contexts and Ubiquitous Models**


-   DDD is primarily about modeling a **Ubiquitous Language** in a **Bounded Context**

-   A Bounded Context is a semantic **contextual boundary**. In other words, a bounded context is defined by a business unit or context where words mean the same thing to every person involved.  (See:<https://martinfowler.com/bliki/BoundedContext.html> for further illustration.)

-   We can further illustrate the idea of a contextual boundary through an example. Imagine a business case where we have both a sales and a support context. In both of these contexts we may have the idea of a product and of a customer. However, what is essential to know about a product or customer in the sales context will be different than what is essential to know about them in a support context. In this case we would have two Bounded Contexts.

-   The Ubiquitous Language consists of the words used inside a Bounded Context and the meaning attached to them. One of the key points about a Ubiquitous Language is that it should be consistent among domain experts, product managers, software engineers and the codebase itself. This extends to the naming of functions, database tables, jobs, etc. In this way communication between all parts of the business unit are facilitated, because everyone is speaking the same language. The only way to arrive at a Ubiquitous Language is through collaborative interaction among all parties.

-   The Ubiquitous Language of the team working in a Bounded Context includes only those concepts that are core to the business concerns of that team, i.e. in-context. This starts with the mental model of the Domain Expert associated with that context.

-   This mental model is best extracted or developed by a discussion between developers and the domain experts, where written specifications are gradually built up by describing how the software should behave and all of its parts--- who, what, when etc. This specification can then be encoded into an executable Specification By Example through unit and acceptance tests.

-   A Bounded Context should have one source code repository, one team working on it, and one set of unit and acceptance tests. One team can work on multiple bounded contexts, but not the other way around. This is because under DDD, understanding the Ubiquitous Language is key to successful design. Multiple teams working on multiple projects will be less likely to succeed in this.

-   If Bounded Contexts are not used, a new software product might become a Big Ball Of Mud, aka the software product will have multiple interrelated, blurry models that are confusing, and also no Ubiquitous Language. This is often the result of not taking heed of domain experts in different functional groups of the business. For instance, in an insurance business the concept of Policy could mean different things to underwriters, claims, and inspections. Mixing them all together could cause the concept to become too bulky and muddled, and therefore the software model and codebase is also bulky and muddled.

-   When a Bounded Context is being developed as part of a major strategic initiative of the organization, it is called the Core Domain. This is the aspect of the business by which it intends to distinguish itself from competition. Part of strategic DDD is identifying what is part of the core domain.

-   Determining if something is part of a Bounded Context is a matter of challenging concepts, rejecting non-essential concepts, and unifying in-context concepts into conceptually simple entities. The end goal should be a number of Bounded Contexts in which all the members have conceptual unity, instead of one large model that refers to itself like a spider-web. Often we start this process by rigorously defining the Core Domain, the rejected concepts from this process will often become Bounded Contexts of their own. Clear interfaces can be imposed on this factored model --- and will be integrated using Context Mapping, which is the subject of a later chapter.

<br>

<br>

## **Chapter Three: Strategic Design With Subdomains**

-   A **Subdomain** is a logically coherent part of the overall business domain for which a product is being designed. It may help elucidate this idea further to consider a subdomain as an "area of expertise" such that a domain expert for the subdomain would be consulted during knowledge acquisition and Product Management. Furthermore, we would ideally have a design where there is one Bounded Context for each subdomain. That is to say, a Bounded Context is the solution space counterpart of a subdomain, which exists in the problem space.

-   The types of Subdomains are: Core domains, Supporting Subdomains, and Generic Subdomains. By identify the type of each Subdomain, we can strategically decide what level of resources to commit to each Bounded Context.

-   A Core Domain is defined by being the key strategic initiative of the business, e.g. the are of the businesses' operations that set it apart from competitors and define its mission. The heaviest investment  is thus made in this subdomain.

-   A Supporting Subdomain is one that supports the Core Domain, but for which no off-the-shelf solutions exist. It is important because the core domain cannot be successful without it, but can be outsourced and should not be invested in too heavily.

-   Generic Subdomains are defined by the fact that they can be outsourced or purchased off the shelf.

-   Subdomains can also be used to reason about legacy systems that have a complex, non-DDD design. If the legacy system ended up becoming a Big Ball Of Mud, we can use Subdomains and subdomain types to decompose it into its constituent parts so it can be more easily reasoned about.

-   As mentioned previously, the ideal case is that we have one software repository per Bounded Context, and one Bounded Context per Subdomain. This is critically important when we are dealing with the Core Domain. If this is not possible for some reason, and we must have more than one Subdomain in one repo, we can achieve some degree of decoupling and separation by splitting the Subdomains into separate software modules.

<br>

<br>

## **Chapter Four: Strategic Design With Context Mapping**

-   When using DDD, each Bounded Context represents the software design solution to the problem space defined by one Subdomain. The model of the Bounded Context itself is based on the Ubiquitous Language, or the language used in each Subdomain and the meaning of its constituent words in the context of that Subdomain. For example in a design case where there is an Sales Subdomain and a Fulfillment Subdomain, there would be a Bounded Context for each and the word "order" would mean different things in the context of each, i.e. different essential pieces of information would be attached to the concept of an order in each context. For example in the Sales context Salesforce id, client, and price would be essential aspects of information, whereas in the Fulfillment context packaging information, shipping deadlines, and addresses would be essential. The process of translating the same word between different contexts is called Context Mapping.

-   Different kinds of Context Mappings are possible. One type is the Partnership Mapping, which requires a large amount of commitment and resources. In this mapping, two teams closely aligned in goals use high communication, continuous integration, and synchronization to keep their mapping in harmony.

-   In the Shared Kernel mapping, two teams would share a small common model that represents the intersection of their Bounded Contexts. This requires a high degree of communication, and a common set of integration and acceptance tests.

-   In the Consumer-Supplier mapping, the Consumer uses whatever is given by the Supplier to perform the mapping. It is up to the Consumer team to ensure they are getting what it necessary from the Supplier. This mapping is a very common use case.

-   A variation of the Consumer-Supplier mapping is the Conformist, where the Supplier has little to no incentive to support the specific needs of the consumer. An example of this could be if an off-shelf solution was used to implement the solution to a Supporting Subdomain, such as using [Amazo](http://amazon.com/)n's models as an affiliate seller.

-   An Anticorruption Layer is the strictest and cleanest Context Mapping, and consists of a fully capable and well-maintained translation between an upstream model and a downstream model, and is capable of translating fully between the two. This is an ideal case, but it requires a large investment of resources.

-   In the Open Host Service, the bounded context is "opened" by giving other contexts access to it as a set of services. It is very easy to "consume" and can easily be paired with a Conformist mapping. Another Context Mapping that is easy to consume is the Published Language, where an interface for a context is defined in XML, JSON or a similar schema-based system. This makes the mapping very easy to produce and consume, and can even be used with an Open Host Service.

-   A sort of counter-mapping is the oft-mentioned Big Ball Of Mud, where a growing number of dependencies across separate contexts create unanticipated complexity. This code then becomes extremely difficult to maintain. One defining feature of a Big Ball Of Mud is that "tribal language" is needed to maintain it, i.e. only developers who have worked on it since its inception understand all the different translations between contexts that occur within it.

<br>

<br>

## **Chapter Five: Tactical Design With Aggregates**

-   With this chapter we move from Strategic Design to Tactical Design, and thus the concepts involved become more practical and less abstract.

-   Martin Fowler's Aggregate definition, which should be read before continuing: <https://martinfowler.com/bliki/DDD_Aggregate.html>

-   An **Entity** is defined as a thing that has a unique identity. We use it here to model things like Product, Post, Release etc. It is not a characteristic of a thing, as this could be non-unique. For example, the color of a Product is not an Entity. Entities are also **immutable**.

-   An **Aggregate** is composed of one or more Entities in a hierarchical relationship, with the premier Entity being termed the Aggregate Root. We can think of the Aggregate Root as "owning" the other Entities in the Aggregate. Another defining feature of an Aggregate is that the Entities it contains should all be consistent with one another in the applications database at all times, in order for business rules to be upheld. For example, in the context of a discussion board product we might have the Entity Thread as the Aggregate Root over the Entity Post. Our business rule might be that each Post is associated to exactly one Discussion, and this rule would be enforced at the transaction level, and also in the design of the database itself. Thus, Aggregates should only be modified and committed to a database in a 1-to-1 relationship with transactions. At the end of each transaction, all business rules must be consistent.

-   The four basic rules of aggregate design are: 1. Protect business invariants inside Aggregate boundaries. 2. Design small Aggregates. 3. Reference other aggregates by identity only. 4. Update other Aggregates using Eventual Consistency.

-   Aggregates and these guidelines could perhaps be best understood by picking a particular implementation of the Aggregate idea, like a relational database table -- or small set of highly dependent tables --- and the corresponding POJO. Other implementations are of course possible, which is why the authors seems to be talking about this subject in a very abstract manner.

-   In the terms of a RDS, our guidelines would translate to 1. Make sure table structures and constraints model business rules and invariants, and that transactions with these tables will ensure these are consistent at all times. 2. Use small, decomposed and normalized tables instead of massive ones. 3. Use Foreign Keys to reference other tables, not duplicate columns etc. 4. Separate responsibility for different Aggregates into different pieces of the application, for example separate DAOs and Managers. If the relationship between two Aggregates that need to be updated occurs across a context boundary, we can use a messaging service to ensure the update occurs while keeping our contexts separate.

-   According to the author, one danger of modeling with Aggregates is that you end up with a bunch of objects that have only accessors but no business logic or behavior, this is called an Anemic Domain Model and is a sign of inadequate business focus during modeling. Since these aggregates are supposed to represent key concepts within the business domain, and also be part of the mental models of domain experts, they should not just be data. However, if a Functional Programming approach is used, this may not be a bad sign as data and behavior should be decoupled therein.

-   A similar point is that the proper level of abstraction for Aggregate design is bounded by the Ubiquitous Language, which once again was developed by consulting with Domain Experts. That is to say, basing abstractions on the business knowledge contained in the Ubiquitous Language will keep abstractions from becoming too abstract. The aggregate models should roughly hew to the mental models of domain experts, or improper abstractions could be the result --- and as we all know, improper abstractions add unnecessary complexity to an application and its code base.

-   In order to obtain a properly-sized aggregate, the author suggests starting out with every Entity as it's own Aggregate, and then building them up into properly sized Aggregates by grouping them whenever business invariants or timing invariants require it.

-   One additional point that should be kept in mind when designing Aggregates is that they should be easily unit testable, and should have their own set of acceptance tests within the broader acceptance tests of the Bounded Context. Right-sized Aggregates will facilitate this by making each Aggregate easily unit testable.

<br>

<br>

## **Chapter Six: Tactical Design With Domain Events**

-   A **Domain Event** is simply a record of something important to the business that occurs in a particular Bounded Context. In a proper DDD design, a Domain Event will often have a 1-1 correspondence with an Aggregate.

-   Domain Events are events as well --- they should be named as a verb in the past tense. We would also record information about them such as the time they occurred.

-   To model a Domain Event, we ask what it should be named but also what properties it should hold. As stated above, we want to record the time that any event occurred. We also want to include any pieces of information (or arguments) that were used to programmatically create the event. So, for instance, if we have a business that is conducting sales, we might have a finalizeSale() function that takes Salesforce information, product ids etc. , we would create from this a Domain Event called SaleFinalized that would record the time of finalization, and all the arguments to the finalizeSale() function.

-   The central utility of using Domain Events is that they allow you publish important events inside of one Bounded Context to other Bounded Contexts. It is therefore the case that this is a type of event-driven and distributed design. By including all necessary information about an event to consumers, along with the time at which this event occurred, we allow the creation of distributed but causally consistent systems by correctly ordering Domain Events inside of different contexts.

-   As mentioned, the idea of supplying Domain Events to consumers is that we can provide information about what occurs in one context to any other, for this reason  only essential information should be included among the Domain Event's properties, and it must be well-named. The combination of the name and properties should make it precisely clear to other contexts what exactly has occurred.

-   When a Domain Event occurs it is often the case that we will also be committing some information to one or more Aggregates. When this is the case, the DomainEvent and modified or created Aggregate should be committed in a single transaction to help ensure causal consistency. The Domain Event is then published or supplied to consumers.

-   In a distributed system, it may be necessary to supply information about what other Domain Event caused the Domain Event being published in order to ensure that consumers can process them in the correct order.

-   In **Event Sourcing**, we do not actually persist the state of Aggregates at all, but only the entire stream of events that have occurred on them, in the correct order. We can then reconstitute Aggregates in the correct state by applying the events to them sequentially. It is important to note here that our Domain Event storage will be append-only, which can make some storage systems very fast and enables Event Sourcing to be a practical solution.

-   Because the entire history of an Aggregate is stored in Event Sourcing, we actually have more information than we would if we simply persisted the state of the Aggregate in a database, for example. This information can be used for debugging, analytics, and compliance analysis.

-   One important note about Event Sourcing is that by recording a Domain Event you are defining a schema based upon your current code. As the code changes, this schema may also change, and these changes must be backwards-compatible somehow. This could impose constraints on future development, or impose migration costs.

<br>

<br>

## **Chapter 7: Acceleration and Management Tools**

-   In a real-world development environment, time constraints are a real, important, and introduce a constant tension between management and developers over what to include in the work of completing a project. Sometimes this tug-of-war can result in the design phase being shortened, or even eliminated altogether. As previously, however, design is inevitable. You can either be conscious of design, and try to make a good one, or end up with a haphazard, random design that was not thought through. This chapter is about techniques for conducting design under tight time constraints.

-   Event Storming is a rapid design process that uses in-person collaboration between engineers, domain experts, and product managers. Event storming meetings happen in a sequence, separated by at least a day. The general idea is to use sticky notes and markers to collaboratively model a business process. By conducting the storming sessions over several days, we can take advantage of the mind's tendency to refine concepts and ideas unconsciously. It is important that everyone involved understand that the first few models in each stage will likely be flawed, wanting to be correct right off the bat is the wrong approach.

-   In the first stage of Event Storming, a particular color of sticky notes is used to chronologically model Domain Events. Next, another color is used to create commands that correspond to each Domain Event. During the second stage it is common for the understanding of the first model (Domain Events) to become refined or change in other ways, this is expected. In the third stage we associate Aggregates to Domain Events and their corresponding commands. Just like in the second stage, we may end up modifying our work from previous stages here as our understanding improves.

-   The fourth stage is defining boundaries and flows between different contexts. These will often occur around departmental divisions, or anywhere that domain experts seem to have different definitions for the same term. This is a clue that you have identified multiple Bounded Contexts. Different contexts are specified by drawing circles around them, and mappings between contexts by arrows or other symbols.

-   This has been a very-high level description of Event Sourcing intended to give a general understanding of the key concepts, the text itself goes into specifics at a much higher level of detail. More research should be conducted before using Event Sourcing in a real-world situation.

-   Another methodology of considerable use here is SWOT Analysis, where SWOT stands for Strengths, Weaknesses, Opportunities, and Threats. Strengths are characteristics of the project that put it in a favorable position relative to other projects. Weaknesses are characteristics that disadvantage this project relative to others. Opportunities are resources or situations that the project could exploit to its advantage, whereas Threats are aspects of the environment that can hinder a project's development. In SWOT analysis we draw four quadrants, one for each category, and brainstorm by putting sticky notes in the relevant quadrant. We can use the information gained from SWOT analysis to better plan a project and improve it likelihood of being completed under time constraints.

-   The final chapter concludes with various tips and tricks for completing modeling under time constraints, estimating time requirements based on the model, and interacting with Domain Experts. These are too varied and specific to be summarized here, but could potentially benefit the developer and should be referenced if using DDD in a production environment.
