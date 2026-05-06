---
title: "SWE: Dynamic-Binding Architectures: Service & Agentic"
description: "Week 12 lecture notes covering SOA, web services, WSDL/SOAP/WS-BPEL, service engineering, agentic AI, & hybrid dynamic architectures."
keywords:
  - "service-oriented architecture"
  - "SOA"
  - "web services"
  - "WSDL"
  - "SOAP"
  - "agentic AI"
  - "distributed systems"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-04-07T11:25-06:00"
---

## agenda

- distributed systems recap
- architecture alternatives (static internal → dynamic agents)
- service-oriented architecture (SOA)
- SOA-related standards: SOAP, WSDL, WS-BPEL
- reusable services & service types
- service engineering & legacy wrappers
- RESTful services vs. SOAP
- ex: car information system
- service testing considerations
- agentic AI
- hybrid dynamic architectures
- managing risk

## distributed systems (ch. 17 context)

building on the [previous lecture](./0331-embedded_systems.md) on embedded
systems & systems of systems, we now zoom out further to consider how sw
components cooperate across networks.

_**distributed system**_ &mdash; a system whose components are deployed on
separate computers that communicate & coordinate via a network. you don't get
to treat them as one monolith.

benefits of distribution:

- _resource sharing_ — hardware, data, & services can be shared across nodes
- _openness_ — standard protocols enable components from different vendors to
  work together
- _concurrency_ — multiple components can do work simultaneously
- _scalability_ — add more nodes to handle more load
- _fault tolerance_ — replication & redundancy let the system survive individual
  component failures

challenges:

- _complexity_ — more moving parts; failure modes multiply
- _security_ — a network boundary is an attack surface; data in transit &
  at rest must be protected
- _harder to manage_ — deployment, monitoring, & debugging are all harder when
  components are physically separated
- _unpredictability_ — network latency, partial failures, & race conditions
  create nondeterminism that's absent in monolithic systems

### middleware

_**middleware**_ &mdash; sw that bridges heterogeneous components & provides
common services so each component doesn't have to reinvent them:

- naming & discovery (find the thing you need)
- transactions (all-or-nothing coordination across components)
- security (authentication, authorization, encryption)
- message passing / RPC (communication primitives)

classic example: CORBA (common object request broker architecture) &mdash;
lets distributed objects communicate regardless of language or platform.
mostly superseded now by web service standards & REST, but the concept lives on.

## who is in control?

before getting to SOA specifically, worth thinking through the _human analogy_
the prof draws on:

humans play various service-related roles:
- take care of our own needs (internal)
- ask for assistance (casual/informal _or_ formal with contract parameters)
- help others when needed

service providing comes w/ expectations: defined parameters, time to complete,
correctness & completeness, reliability & consistency. these exact same
expectations transfer to sw systems.

when our system calls an external service:
- _we_ perceive ourselves to be in control
- control is _temporarily_ handed to the partner at our request
- control returns when the partner completes its finite processing

things that can go wrong (& how to manage them):

- can't do it ourselves → call a lifeline (external service)
- call not answered → call another one
- provider unavailable → call another one
- provider agrees but fails to deliver → call another one
- no more providers → do it ourselves, or retry later

that last bullet is why _exception management_ is a first-class design concern,
not an afterthought.

## architecture alternatives

> [!TODO]
>
> add diagram here showing the four architecture alternatives on a
> static-to-dynamic / internal-to-external 2×2 grid

four flavors, roughly in order of increasing dynamism:

- _**static & internal**_ — functions/methods/routines within our own system;
  we designed, implemented, & tested them; fully predictable
- _**static & external (traditional partners)**_ — live at the fringe of our
  context model; established protocols govern control; reliability concerns
  because "we didn't build it," but at least the binding is fixed at design time
- _**dynamic service providers (SOA)**_ — find potential partners _as needed_,
  request binding at runtime; partners certified as predictably reliable;
  manage risks w/ exception management; binding is dynamic but services are
  well-defined
- _**dynamic agents**_ — control agent finds partner agents when needed; manages
  temporary relationships; _non-deterministic_, least predictable/knowable/
  controllable; most powerful & most risky

## service-oriented architecture (SOA)

_**SOA**_ &mdash; an architectural style based on the notion of cooperating
entities (services) that offer to perform well-defined operations & make
information available in a controlled, managed way.

key properties:

- defined interfaces must be _published_ (discoverable)
- services are _loosely coupled_ — a service consumer doesn't need to know
  how the service is implemented, only what it does & how to call it
- enables creation of _configurable, distributed, platform-independent_ systems
- supports _reuse_ — once a service exists, any number of systems can use it

> [!TODO]
>
> add SOA overview diagram here — showing service consumer, service registry
> (UDDI), service provider, & the publish/find/bind triangle

benefits of SOA:

- services can be provided locally _or_ outsourced to external providers
- services are _language-independent_ (interface is the contract, not the impl)
- investment in legacy systems can be preserved (wrapper pattern)
- inter-organizational computing facilitated through simplified information
  exchange
- reuse across systems & organizational boundaries

### SOA-related standards

three core standards you need to know:

_**SOAP**_ (SOA protocol) &mdash; message interchange format; supports
communication between services; XML-based; relatively heavyweight.

_**WSDL**_ (web services definition language) &mdash; service interface
definition; specifies:
- _What_ — interface description (operations, input/output types)
- _How_ — details of how to communicate (binding: SOAP over HTTP, etc.)
- _Where_ — location of the implementation (endpoint URL)

_**WS-BPEL**_ (web services business process execution language) &mdash;
workflow language; lets you compose multiple services into a higher-level
business process; specifies _orchestration_ (one coordinator directs others).

> [!TODO]
>
> add WSDL document structure diagram here — showing types, messages,
> portType (interface), binding, & service elements

_**UDDI**_  (universal description, discovery & integration) &mdash; the
service registry / "yellow pages" for web services; lets consumers discover
available services dynamically. largely fell out of favor in practice (most
discovery happens via documentation or API portals), but the concept matters
for understanding dynamic binding.

### RESTful services

SOAP/WSDL is the "heavy" stack. RESTful services are the simpler alternative:

- uses standard HTTP verbs: GET (read), POST (create), PUT (update),
  DELETE (remove)
- returns JSON or XML
- _stateless_ — each request carries all context needed; server holds no
  session state between calls
- simpler to implement & consume; dominant in modern web APIs
- tradeoff: less formal contract than WSDL; tooling for discovery & validation
  is less standardized

## reusable services

once a service is well-established:
- any number of systems can use it
- well-defined interface; consistent, reliable performance; independent &
  loosely coupled
- this is the SOA pitch for _reuse_ — build once, use everywhere

### service types

_**utility services**_ &mdash; general functionality not tied to a specific
business domain (e.g., currency conversion, unit conversion, address validation)

_**business services**_ &mdash; associated w/ a specific business function
(e.g., student registration, invoice processing, inventory check)

_**coordination/process services**_ &mdash; support more general business
processes by orchestrating other services (e.g., procurement process management,
order fulfillment pipeline)

## ex: car information system

a good concrete illustration of dynamic binding in SOA:

- not necessary to decide at programming or deployment time which information
  service provider should be used
- as the car moves around, the in-car sw uses a _service discovery service_
  to find the most appropriate local information service & binds to it at runtime
- a _translation service_ allows crossing language borders — making local
  information available to drivers who don't speak the local language

> [!TODO]
>
> add car information system architecture diagram here — showing in-car sw,
> service discovery, local information services (in multiple regions), &
> translation service

this example shows why dynamic binding matters: a static binding chosen at
deploy time would require knowing in advance which service to use in every
possible location — obviously impractical.

## service engineering

_**service engineering**_ &mdash; the process of developing services for reuse
in service-oriented applications.

because a service must work for many different consumers (not just one system),
design is harder than for a one-off component:

- must be designed as a _reusable abstraction_ usable in different systems w/
  different contexts
- _generally useful functionality_ must be designed — not too narrow, not too
  broad
- must be _robust & reliable_ — any consumer depends on it; failures cascade
- must be _documented_ so it can be discovered & understood by potential users

steps:

1. _candidate service identification_ — what functionality is general enough
   to be a standalone service?
2. _interface specification_ — write the WSDL (or OpenAPI/REST equivalent);
   inputs, outputs, errors
3. _implementation_ — build it; should be independent of any particular consumer
4. _test & certify_ — verify correctness & reliability before publishing
5. _publish_ — register with discovery mechanism; document for consumers

### legacy system wrappers

a key SOA pattern: rather than rewriting (or decommissioning) a legacy system,
_wrap it_ with a service interface.

- extend the life of legacy systems
- expose legacy functionality via a modern, standard interface
- consumers see the wrapper's interface; implementation details of the legacy
  system are hidden
- useful when rewriting is too risky or expensive but the functionality is still
  needed

## service testing considerations

testing service-based systems is meaningfully harder than testing monolithic sw:

- _control/access determined by service provider_ — you can't instrument or
  inspect the service's internals
- _application may not always use the same service_ — dynamic binding means
  the service selected at runtime may differ between test runs; different
  providers may behave differently
- _performance differs under varying loads_ — a service that performs well in
  isolation may degrade when serving many consumers simultaneously
- _testing exception handling may depend on actual service failures_ — hard
  to trigger reliably; may need to use stubs that simulate failures

approaches:
- _stubs_ — fake service implementations that return canned responses; enable
  unit-level testing of the consumer
- _live service testing_ — test against the real service; reveals real
  performance & failure modes but introduces dependency on external availability

## agentic AI

_**autonomous agents**_ &mdash; goal-oriented sw entities that:

- are aware of their environment (perceive state)
- are able to reason & make decisions
- (presumably) take the best actions for achieving stated goals
- learn & adapt over time
- operate in an inherently uncertain future

this is qualitatively different from SOA: an agent doesn't just _respond_ to
requests — it _pursues goals_ over time, managing its own sub-goal selection,
partner selection, & response to unexpected situations. the pursuit is
_open-ended_, not bounded by a finite transaction.

> [!NOTE]
>
> "agentic AI" is a broad term. at the architectural level, what matters is
> that an agent can dynamically identify what it needs, find partners (services,
> tools, other agents) to help, evaluate results, & adjust — without a human
> in the loop for each step.

## hybrid dynamic architectures

the practical answer for most real systems: combine SOA & agentic AI at the
appropriate layers.

- _**SOA for the foundation**_: data management; basic communication & control;
  the predictable, reliable, well-defined plumbing
- _**agentic for decision-making & learning**_: understanding current state;
  predicting needs; finding & binding to services dynamically; assessing success
  in meeting goals; learning to be better (including potentially discovering
  new goals)

> [!TODO]
>
> add hybrid architecture diagram here — showing SOA layer (services, registry,
> standard protocols) underneath an agentic layer (goal manager, planner,
> service selector, evaluator, learner)

the hybrid approach lets you get the _predictability_ of SOA where you need it
& the _open-ended adaptability_ of agents where that's valuable.

## managing risk

with dynamic binding (especially agentic), risk management becomes central:

- use the approach that best fits the need:
  - need for _predictability_ → lean toward SOA or static external
  - _open-ended pursuit of goals_ → agentic
  - _tolerance for delays_ & _acceptance of the unknown_ drive the tradeoff
- develop _exception management_ for all system-partner interactions:
  - _binding_ — what if we can't find or bind to a service?
  - _parameter passing_ — what if the interface version doesn't match?
  - _timeouts_ — what if the partner doesn't respond in time?
  - _lack of availability_ — what if the provider is down?
- proactive & reactive QA:
  - _registration based on certification_ — only certified services enter
    the registry; reduces risk of binding to unreliable providers
  - _protocols_ — well-defined interaction patterns reduce ambiguity
  - _test thoroughly_ — especially exception paths & failure modes
