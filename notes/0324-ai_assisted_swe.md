---
title: "SWE: AI Assisted Software Engineering"
description: "Week 10 lecture notes covering AI-assisted swe, automation, sw reuse, component-based engineering, the Ariane 5 case study, & ERP systems."
keywords:
  - "AI assisted software engineering"
  - "software reuse"
  - "component-based software engineering"
  - "CBSE"
  - "Ariane 5"
  - "ERP"
  - "automation"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-03-24T11:25-06:00"
---

## agenda

- human sw engineering: creation & professional society
- self-reflection: managing risk of human error
- computer-assisted swe tools
- AI-assisted swe opportunities
- content creation w/ AI
- automation: benefits & conditions
- reuse: concept & benefits
- case study: Ariane 5 launcher failure
- rapid iteration: benefits & challenges
- incremental dev vs. prototyping
- reuse opportunities & approaches
- ERP systems
- component-based sw engineering (CBSE)
- component models & challenges

## human sw engineering

continuing from [previous lecture](./0310-evolution_and_resilience.md) on
sw evolution & resilience, we now zoom out to ask: how do _humans_ produce
sw, & how can we make that process better?

### creation

sw engineers aren't born knowing how to build reliable systems — the craft
is developed through:

- _education & mentoring_ — formal training plus apprenticeship w/ experienced
  engineers; tacit knowledge transferred person-to-person
- _skill development & experience_ — deliberate practice; exposure to diverse
  problem domains
- _learning by doing_ — can't truly learn swe from a textbook alone; must
  build & fail & fix
- _commitment & discipline_ — consistent application of good practices even
  under pressure; the habits that separate professionals from amateurs

### professional society

the swe profession is supported by institutions that codify & maintain standards:

- _**standards**_ — IEEE, ISO/IEC provide interoperability & quality benchmarks
- _**training & certification**_ — structured pathways to demonstrate competence
- _**ethics**_ — ACM & IEEE codes of ethics establish obligations to users,
  employers, & society; not just a formality

## self-reflection: managing risk of human error

humans make mistakes. sw engineers are human. therefore sw engineers make
mistakes. this is not a character flaw — it's a fundamental property of the
human cognitive system.

strategies for managing this reality:

- _**oversight & ongoing development**_ — pair reviews, code review, independent
  QA; continuous learning to improve individual skill
- _**case studies & root-cause analysis**_ — learning from past failures;
  blameless post-mortems that identify systemic causes rather than scapegoating
  individuals
- _**best practices & shared knowledge**_ — documented patterns, style guides,
  checklists; codified institutional memory
- _**carrots & sticks**_ — incentives (recognition, career growth) for quality;
  consequences for negligence; neither alone is sufficient

> [!NOTE]
>
> the goal of automation is often framed as _removing_ human fallibility from
> the loop. but as we saw in the previous AI lecture, automation introduces its
> own failure modes — and can degrade human ability to intervene when it fails.
> the better framing: use automation to _extend_ human capability while
> maintaining meaningful oversight.

## computer-assisted swe

before we get to AI, it's worth noting the long history of tools that have
already automated or assisted parts of the swe process:

- _**higher-level languages & compilers**_ — programmer works at a higher level
  of abstraction; compiler handles the translation to machine code; massive
  productivity gain over assembly
- _**IDEs**_ — syntax highlighting, auto-complete, inline error detection,
  refactoring tools; reduce cognitive load for routine tasks
- _**requirements traceability tools**_ — link reqs to design elements to test
  cases; maintain consistency across the lifecycle
- _**modelling & design tools**_ — UML editors, ERD tools, architecture
  diagramming; support communication & design validation
- _**automated testing**_ — unit test frameworks, CI pipelines, test coverage
  analysis; dramatically reduce the cost of regression testing
- _**change control & management**_ — version control (git), issue tracking,
  change control boards; make change tractable
- _**documentation tools**_ — javadoc, swagger, wiki platforms; reduce friction
  in keeping docs current

## AI-assisted sw engineering

AI extends computer assistance into areas that require more judgment:

- _**best practices & past history**_ — mining historical project data to
  identify patterns that predict success or failure; recommending practices
  tailored to current project context
- _**planning including risk management**_ — AI-assisted estimation; risk
  scoring based on project characteristics
- _**reuse & automation opportunities**_ — identifying where existing components
  could be leveraged; suggesting similar past solutions
- _**defect anticipation, discovery, & removal**_ — static analysis + ML to
  predict defect-prone code areas before testing; automated bug triaging
- _**test planning**_ — data generation, test case creation, automated test
  execution & result analysis
- _**modelling & simulation**_ — AI-assisted generation of system models; running
  simulations to explore design alternatives before committing to implementation

### AI content creation

AI is increasingly used to _generate_ sw artifacts, not just assist in analyzing
them:

- requirements specification drafts
- design documentation
- test plans & test cases
- _code_ (LLM-based code generation)
- communication support (meeting summaries, stakeholder reports)
- project support (status updates, risk registers)
- collection of history (change decision rationale, ADRs)
- project & process documentation

> [!WARNING]
>
> AI-generated content requires human review. AI can generate plausible-looking
> artifacts that contain subtle errors — incorrect requirements, flawed test
> cases, buggy code. "it looks right" is not the same as "it is right." treat
> AI output as a first draft written by a fast but fallible junior engineer.

## automation

_automation_ = computers doing what humans used to do.

### benefits of automation

- _**speed**_ — machines execute faster than humans
- _**reliability**_ — always follow the rules; no variation between instances
- _**robustness**_ — never tired, bored, or distracted
- _**cost**_ — don't get paid per hour; scales without proportional labor cost

### conditions for successful automation

sw engineers create a system which follows the steps of a given process. this
works better when:

- steps are _well-defined_ — ambiguous processes resist automation
- steps are _simple to understand_ — complexity increases implementation risk
- steps are _not likely to change_ — automation is an investment; volatile
  processes make that investment quickly obsolete

## reuse

_**reuse**_ &mdash; taking a previously produced artifact & using it in future
development efforts.

better: _creating artifacts which are measurably reusable_ — designed from the
start to be used again w/ minimal modification.

### benefits

- _speed_ — don't rebuild what already works
- _peace of mind_ — known quantity; someone else has already debugged it
- _reliability_ — reused components already tested & field-proven
- _reduced risk_ — less new code = fewer opportunities for new defects
- _ease of maintenance_ — shared components mean shared maintenance burden

### conditions for successful reuse

sw engineers design artifacts for reuse when the artifact:

- addresses a _well-defined problem_ — generic enough to recur, specific enough
  to be directly applicable
- is _self-contained (modular)_ — minimal external dependencies; doesn't drag
  in unneeded complexity
- is _likely to be needed again_ — not so niche it will never recur
- is _easy to "find"_ — discoverable; with a well-defined interface that makes
  its purpose clear

## case study: Ariane 5 launcher failure

> [!TODO]
>
> add Ariane 5 explosion diagram / timeline here

### what happened

- reuse plan: inertial reference sw from Ariane 4 was reused in Ariane 5
- the reused code contained "extras" — functionality not required for Ariane 5
- Ariane 5 had more powerful engines → generated larger numbers than Ariane 4
  ever had
- the "extra" code attempted to convert a 64-bit floating-point number to a
  16-bit integer; the number was too large; an exception was generated
- the exception handler shut down the inertial reference system
- w/out inertial reference, the rocket self-destructed on its maiden flight

### why it failed

- the extra code had _never been tested_ in the Ariane 5 context — because it
  wasn't required for Ariane 5, it was not in scope for testing
- the assumption was: "it worked before" — but _context changed_ in a way that
  made previously safe code dangerous

### lesson

> **reuse requires careful analysis of the new context.**
> "it worked before" is not sufficient justification for reuse.

before reusing a component:

1. understand _all_ of what the component does (including the "extras")
2. analyze whether the new context introduces any inputs or conditions outside
   the range the component was designed for
3. test the component _in the new context_, not just in the original one
4. remove or disable functionality not needed in the new context

## benefits of rapid iteration

why iterate quickly rather than build the whole thing first?

- _**reduce opportunity for change**_ — customer needs evolve; business &
  competitive demands shift; technology advances. shorter cycles mean the system
  adapts before requirements drift too far from the implementation
- _**focus on what is known**_ — complete understanding of a complex system is
  difficult to achieve before significant progress has been made; better to
  implement what's understood now & learn from real feedback
- _**user involvement**_ — shorter cycles create more & better opportunities to
  get real users in front of working sw; reduces risk of building the wrong thing
- _**business risk reduction**_ — delivering value incrementally means early
  delivery of partial value; catastrophic failure of the whole project becomes
  less likely

## challenges of rapid iteration

rapid iteration is not free:

- _**difficult to maintain discipline**_ — perception that formal processes "take
  too long" under deadline pressure; temptation to cut corners w/ "we'll catch
  it on a future iteration" (technical debt accumulates)
- _**overly narrow focus**_ — each iteration is necessarily small; easy to lose
  sight of the "big picture" architecture; technical investments (new tools,
  architectural improvements) compete for iteration capacity & often lose

## incremental dev vs. prototyping

two related but distinct approaches:

_**incremental development**_ &mdash; series of planned, relatively small
efforts designed to result in a complete system meeting user spec. each
increment is potentially shippable. the plan spans the full scope.

_**prototyping**_ &mdash; can _facilitate_ incremental development by
incrementally improving a prototype into a finished system. two varieties:

- _evolutionary prototyping_ — prototype _is_ the system; refined until it
  meets requirements
- _throw-away prototyping_ — "quick & dirty" implementation used as a
  communication vehicle or R&D tool; explicitly intended to be discarded;
  akin to research; helps clarify requirements before real implementation

the risk w/ throw-away prototypes: they have a tendency to become production
systems. discipline required.

## reuse opportunities

reuse is possible at multiple levels of granularity:

> [!TODO]
>
> add slide diagram showing reuse opportunities spectrum here (from individual
> classes/functions up through components, frameworks, & full applications)

spectrum (roughly, smallest to largest granularity):

- _test classes & procedures_ — utility functions, data structures
- _components_ — CBSE-style reusable building blocks (see below)
- _libraries_ — curated collections of components w/ defined APIs
- _frameworks_ — abstract application architectures; concrete implementation
  via configuration & extension
- _COTS products_ — full commercial applications integrated as-is or w/ adapters
- _application system products_ — full systems licensed & configured for
  specific organizational needs

### other reuse approaches

- _**generator-based reuse**_ — CASE tool recognizes opportunities & generates
  boilerplate code; templating engines, scaffolding tools
- _**COTS products**_ — using existing commercial products; may require
  compromising on requirements to fit the product; integration is the challenge
- _**application frameworks**_ — objects may be too specific; frameworks provide
  a collection of classes & defined interfaces between them; three categories:
  - _system infrastructure_ — OS abstraction, comms, UI toolkits
  - _middleware integration_ — enterprise service buses, message queues
  - _enterprise application (ERP)_ — full business process frameworks

## ERP systems

_Enterprise Resource Planning_ systems are a canonical example of large-scale
reuse: a vendor-provided framework that implements common business processes.

structure:

- _modules_ to support different business functions (finance, HR, supply chain,
  manufacturing, CRM)
- _defined business processes_ associated w/ each module — the vendor's
  opinionated model of how these processes work
- _common database_ maintaining information about all related business functions;
  single source of truth across modules
- _business rules_ applying to all data — encoded constraints that enforce
  organizational policies

### ERP configuration

organizations don't get a blank slate — they configure the ERP to their needs:

- selecting required functionality (which modules?)
- establishing the data model (what entities? what relationships?)
- defining business rules (what constraints apply?)
- defining expected interactions w/ external systems
- designing input forms & output reports
- designing new business processes that _conform to_ the underlying process model

> [!TODO]
>
> add ERP architecture diagram from slides here

> [!NOTE]
>
> this last point is critical — often the org must _change its processes_
> to fit the ERP, not the other way around. this is one of the most
> organizationally disruptive aspects of ERP implementation.

## component-based sw engineering (CBSE)

_**CBSE**_ &mdash; the process of defining, implementing, & integrating
loosely coupled independent components into larger systems.

components sit between objects & applications in scale:
- _too small_ = objects (too fine-grained for independent deployment)
- _too large_ = full applications (can't compose them easily)
- _just right_ = components (independently deployable, well-defined interfaces)

### reusable component requirements

a proper reusable component:

- conforms to a standardized model enforcing interfaces, documentation,
  & deployment packaging
- exists independent of other components (minimal coupling)
- has strictly controlled public access — only via defined interfaces
- is deployable as a standalone entity
- is fully documented including both _syntax_ (what the interface looks like)
  & _semantics_ (what it does; pre/post conditions; exceptions)
- defined by two interface types:
  - _**provides interface**_ — services the component offers to clients
  - _**requires interface**_ — services the component needs from its environment

### component models

standards that ensure interoperability between components from different sources:

- _CORBA_ — language-neutral middleware standard; Interface Definition Language
  (IDL) for cross-language component interaction
- _Java Beans / J2EE_ — Java-ecosystem component model; EJBs for enterprise
  services
- _COM+ / .NET_ — Microsoft's component model; cross-language within the .NET
  ecosystem

elements standardized by component models:

- _interfaces_ — operation names, parameters, exceptions; expressed in IDL
- _information_ — naming conventions, metadata, customization parameters
- _deployment_ — packaging format; installation & configuration process

### CBSE process

1. _components specification_ — define what the component does & its interfaces
2. _component search_ — find existing components that match the need
3. _component validation_ — verify the found component actually does what's
   needed in _this_ context (Ariane 5 lesson applies here)
4. _system composition_ — connect components; handle middleware; adapt
   interfaces where needed

### challenges of component-based reuse

CBSE is not a free lunch:

- _**complexity**_ — understanding component interactions & dependencies is hard
- _**trust**_ — can you trust a third-party component? how was it tested?
  what are its failure modes?
- _**tight coupling w/ specific applications**_ — components designed for one
  context may resist reuse in another
- _**maintainability**_ — when the component vendor updates (or abandons) the
  component, what happens to your system?
- _**customization costs**_ — adapting a component that's "almost right" can
  cost more than building from scratch in the worst case
- _**inconsistency**_ — components from different vendors may have incompatible
  assumptions about data formats, error handling, threading models
