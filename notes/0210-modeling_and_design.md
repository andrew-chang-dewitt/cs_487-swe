---
title: "SWE: Modeling & Architecture"
description: "Week 5 lecture notes covering system modeling, architectural design, & design patterns — UML diagrams, architectural styles, & design-to-implementation concerns."
keywords:
  - "system modeling"
  - "architectural design"
  - "design patterns"
  - "UML"
  - "software architecture"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-02-10T11:25-06:00"
---

## agenda

- what is modeling & why it matters
- context models
- interaction models (use cases & sequence diagrams)
- structural models (class diagrams, generalization, aggregation)
- behavioral models (data-flow & state machines)
- data models & data dictionaries
- design patterns
- design to implementation
- architecture: levels of abstraction & benefits
- architectural patterns
  - layered
  - repository
  - client-server
  - pipe-and-filter
- application architectures
- modular decomposition styles
- control styles
- distributed systems

## modeling

building on the [previous lecture](./0203-pro_re_active_qa.md) on QA, this week
we move into the design phase and start asking: how do we represent what we're
building before we build it?

_**system modeling**_ &mdash; the process of creating abstract representations
of a system, each capturing a different perspective or level of detail. models
aren't the system — they're tools for _thinking about_ & _communicating about_
the system.

why model at all? words alone have limited effectiveness when describing complex
systems — ambiguity creeps in, stakeholders interpret things differently, & big
pictures get lost in prose. models bridge the gap from analysis to design by
giving everyone a shared visual language.

three main perspectives a set of models should cover:

- _external context_ &mdash; what's the system's environment?
- _system behavior_ &mdash; how does the system respond to inputs & events?
- _architecture_ &mdash; how is the system structured internally?

UML (Unified Modeling Language) is the de facto standard for sw modeling. the
diagrams we'll look at this week all come from or are inspired by UML:

- use case diagrams
- sequence diagrams
- class diagrams
- state diagrams
- activity diagrams

## context models

before you can design anything, you need to know _where the system ends and its
surrounding environment begins_. that's what context models do.

key questions a context model answers:

- what's inside the system boundary vs. what's external?
- what interfaces does the system expose to the outside world?
- are related components inside the boundary or accessible only through defined
  interfaces?

important nuance: boundaries aren't purely technical decisions. business rules,
regulatory constraints, & user/organizational constraints all shape where the
line gets drawn. don't assume the "obvious" technical boundary is the right one.

## interaction models

_**interaction models**_ capture how the system interacts with external actors
or how internal components interact with each other. two main flavors:

### use case diagrams

each use case represents a discrete external interaction — a single, coherent
thing a user (or another system) can do with your system. use cases are:

- very high level (not implementation detail)
- focused on _what_, not _how_
- a useful tool for scoping & communicating with stakeholders

> [!TODO]
>
> add use case diagram example from slide 8 here

### sequence diagrams

sequence diagrams capture _the order of interactions_ — who sends what message
to whom, & in what sequence, for a given use case. they're great for:

- tracing through a single use case end-to-end
- making timing & ordering dependencies explicit
- spotting integration concerns between components

> [!TODO]
>
> add sequence diagram example from slide 9 here

## structural models

_**structural models**_ capture the components of a system & their
inter-relationships — the static "shape" of the system.

### class diagrams

OO class diagrams show:

- classes (templates for objects)
- attributes & operations on each class
- relationships between classes: association, generalization, aggregation

the goal is to model the "real world" — things, their properties, & how they
relate. keeping the model close to the real world has practical benefits:

- users can actually understand it (& give useful feedback)
- higher reuse potential — natural structures tend to generalize well
- behavior & interfaces feel more intuitive

> [!TODO]
>
> add class diagram example from slides 12–15 here

### generalization

_**generalization**_ &mdash; using more general/abstract terms for groups of
things that share common characteristics. maps directly to inheritance in OO
languages. benefits:

- reduces duplication
- makes common behavior & attributes explicit
- makes extension & modification easier

### aggregation

_**aggregation**_ &mdash; building complex components from sub-components. a
"has-a" relationship. models how real-world things are composed of parts. also
supports reuse — if sub-components are well-defined, they can be recombined in
new ways.

## behavioral models

behavioral models capture _how the system acts_ — what it does with data, &
how it responds to events.

### data-flow models

data-flow diagrams (DFDs) model the flow of information through a system:

- where does data come from?
- who "owns" it?
- how is it processed, transformed, or disseminated?

these are more about _work_ than _structure_ — useful for capturing business
processes & understanding how data moves through an organization.

### state machine / event-driven models

state diagrams model systems that move from state to state in response to events
(stimuli). useful for:

- capturing event-driven behavior precisely
- asking "what happens if _this_ event occurs in _this_ state?"
- identifying missing handlers for unexpected events

> [!TODO]
>
> add state machine diagram example (microwave) from slide 17 here

## data models

_**data models**_ give a more static view of information than DFDs — focused on
the relationships among information types (entity-relationship models).

why they matter:

- critical design decisions start to crystallize here: unique identifiers, data
  types, cardinality of relationships
- _**data dictionary**_ &mdash; an alphabetic listing of data entities & their
  descriptions; keeps everyone using the same vocabulary

## design patterns

_**design patterns**_ are common, proven solutions to common design problems.
the concept was adopted from the building architecture community in the early 90s
by the "Gang of Four" (Gamma, Helm, Johnson, Vlissides).

the pitch:

- why reinvent the wheel? common problems have been solved before
- patterns are already proven & tested in other contexts
- significant up-front time savings
- avoids the fix-retest cycle that comes w/ novel solutions

classic examples:

- _**observer**_ &mdash; separate the display of an object's state from the
  object itself; multiple views can observe the same model (slides call this out
  specifically)
- _**facade**_ &mdash; simplify a complex subsystem behind a clean interface
- _**iterator**_ &mdash; provide a standard way to traverse a collection
- _**singleton**_ &mdash; ensure only one instance of a class exists

> [!TODO]
>
> add observer pattern diagram from slide 20 here

## from design to implementation

bridging the gap from design artifacts to running code involves three main concerns:

### reuse

levels of reuse available:

- design patterns (discussed above)
- OO design (well-designed classes & hierarchies reused across projects)
- reusable components (libraries, modules w/ clean interfaces)
- reusable systems &mdash; tailored COTS (Commercial Off-The-Shelf) products

open-source has dramatically expanded what's available for reuse. the tradeoff:
open-source reuse requires understanding the license & accepting dependency on
an external codebase you don't fully control.

### configuration management

everything that goes into the system should be under version control &mdash;
not just code, but requirements docs, design models, test plans, & build scripts.
the key activities:

- version control (git etc.)
- system build management (CI/CD pipelines)
- issue/change management

this connects back to last week's CM discussion.

### host-target development

dev environment ≠ production environment. key considerations:

- configure the dev host to match the target as closely as possible
- use simulation/emulation for testing when the target isn't available
- particularly critical for embedded systems where the "target" might be
  specialized hardware

## architecture

_**software architecture**_ &mdash; the high-level structure of a sw system:
the significant decisions about organization, the selection of structural
elements & their interfaces, & the patterns that guide the composition of those
elements.

two levels of abstraction in the slides:

- _program-level ("small")_ &mdash; internal structure of a single application
- _system/enterprise-level ("large")_ &mdash; how multiple systems interact

### why bother defining architecture?

three big benefits:

- _communicating w/ stakeholders_ &mdash; architecture diagrams let non-technical
  stakeholders see the big picture without drowning in implementation detail
- _completing analysis_ &mdash; working through architecture forces you to resolve
  ambiguities left over from requirements
- _facilitating large-scale reuse_ &mdash; well-defined architectures can be
  reused across projects w/ similar structural needs

### requirements & architecture

non-functional requirements (NFRs) are largely satisfied (or not) at the
architecture level — _not_ at the code level. NFRs that architecture primarily
affects:

- _performance_ &mdash; structure determines data flow & latency
- _security_ &mdash; where assets live & how they're accessed
- _safety_ &mdash; redundancy, isolation, fail-safe defaults
- _availability_ &mdash; how failures propagate & whether system survives them
- _maintainability_ &mdash; how easy it is to change a part w/o breaking others

tradeoffs are almost always necessary. performance & security often conflict:
encryption adds overhead. availability & security conflict: redundancy means
more attack surface.

### key design decisions

when doing architectural design, you're making decisions like:

- can an existing generic application architecture be reused, or do we need
  something custom?
- how will the system be distributed across multiple processors?
- what architectural styles or patterns fit this system's needs?
- how are structural elements decomposed into modules?
- what's the strategy for controlling operation (centralized vs. event-based)?

### architectural views

no single diagram captures everything. the book describes five views:

- _logical_ &mdash; system as interacting objects
- _process_ &mdash; interacting processes (concurrent behavior)
- _development_ &mdash; components to be developed (useful for team planning)
- _physical_ &mdash; interacting hw & sw (deployment)
- _conceptual_ &mdash; basis for decomposing high-level requirements

## architectural patterns

just as design patterns capture reusable solutions at the code level,
_**architectural patterns**_ capture reusable solutions at the structural level.

### layered architecture

_**layered architecture**_ &mdash; system organized into hierarchical layers;
each layer provides services to the layer above & consumes services from the
layer below.

benefits:

- separation & independence (change one layer w/o touching others — if interfaces
  are respected)
- supports incremental development (can build & test layer by layer)
- well-understood & widely applicable (OSI network model, MVC, etc.)

> [!TODO]
>
> add generic layered architecture diagram from slide 27 here

### repository architecture

_**repository architecture**_ &mdash; a central shared repository holds all
data; sub-systems communicate by reading & writing to it rather than directly
to each other.

good for:

- systems where large amounts of shared data must be managed consistently
- supporting information exchange between loosely coupled sub-systems

> [!TODO]
>
> add repository architecture diagram from slide 28 here

### client-server architecture

_**client-server**_ &mdash; a set of services offered by servers; clients
access those services over a network.

two variants:

- _thin client_ &mdash; everything except presentation logic runs at the server
- _fat client_ &mdash; everything except data management runs at the client

> [!TODO]
>
> add client-server diagram from slide 29 here

### pipe-and-filter architecture

_**pipe-and-filter**_ &mdash; data flows through a pipeline of transformations.
each "filter" processes & transforms the data; "pipes" connect them.

classic example: Unix command line (`cat file | grep pattern | sort | uniq`).
good for:

- data processing workflows
- compilers (lexer → parser → semantic analysis → code gen)

> [!TODO]
>
> add pipe-and-filter diagram from slide 30 here

## application architectures

different problem domains have recognized architectural patterns:

- _data-processing applications_ &mdash; batch processing of large datasets
- _transaction-processing applications_ &mdash; database-backed systems w/ ACID
  guarantees
- _event-processing systems_ &mdash; react to streams of events in real or near
  real time
- _language-processing systems_ &mdash; compilers, interpreters, NLP pipelines

## modular decomposition styles

two dominant styles for breaking a system into modules:

- _**object-oriented decomposition**_ &mdash; loosely coupled objects w/
  well-defined interfaces; classes are templates for instances. best for reuse —
  OO structures map well to how the _real world_ is organized
- _**function-oriented pipelining**_ &mdash; data flow; inputs processed by
  transformational functions to produce outputs. best fit for how _work_ is
  organized — cleaner for data-processing workflows

real systems often blend both: OO for domain modeling, functional pipelines for
data processing components.

## control styles

- _**centralized control**_ &mdash; one sub-system controls the others;
  single point of design & coordination; simpler to reason about but a potential
  bottleneck & single point of failure
- _**event-based control**_ &mdash; each sub-system reacts to events from a
  shared bus or environment; often a more natural fit for real-world behavior;
  harder to reason about & trace causally

## distributed systems

### benefits & tradeoffs

_**distributed systems**_ spread computation across multiple processors/machines.
benefits:

- shared resources (storage, compute, services)
- open/standard-driven interfaces
- concurrency & parallelism
- scalability
- fault tolerance

but also significant costs:

- complexity (failure modes multiply)
- security vulnerabilities (more attack surface, more network exposure)
- harder to manage & monitor
- unpredictability (network latency, partial failure)

### distributed system patterns

- _**master-slave**_ &mdash; real-time systems requiring guaranteed response
  times; master delegates tasks to slaves & aggregates results
- _**2-tier client-server**_ &mdash; centralized; simpler to secure; classic
  database-backed app
- _**multi-tier C/S**_ &mdash; high-volume transaction processing; separates
  presentation, business logic, & data tiers
- _**distributed component**_ &mdash; combining resources from different systems
  (think microservices or CORBA-style middleware)
- _**peer-to-peer**_ &mdash; servers "introduce" peers who then collaborate
  locally; no central server required for ongoing operation
