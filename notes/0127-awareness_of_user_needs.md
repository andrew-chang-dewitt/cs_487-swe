---
title: "SWE: Awareness of User Needs"
description: "Week 3 lecture notes covering requirements engineering — defining, capturing, & validating user & system requirements."
keywords:
  - "requirements engineering"
  - "functional requirements"
  - "non-functional requirements"
  - "elicitation"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-01-27T11:25-06:00"
---

## agenda

- requirements defined
  - user vs. system requirements
  - types: functional, non-functional, domain
  - types of non-func reqs
- user req challenges
- capturing reqs (H-H-I)
- system req challenges
- specification notations
- interface specification
- the requirements document
- requirements engineering process
  - feasibility studies
  - elicitation & analysis
  - requirements discovery
  - ethnography
- requirements validation

## requirements defined

the _**requirements**_ for a sw system establish the needs of the user &
the constraints of the environment in which the system must operate. the
book draws a useful distinction between two levels of formality:

- early on, reqs are left somewhat open to interpretation &mdash; useful
  when bidding on contracts, where you don't want to over-specify & lock
  yourself in before scoping is done
- later, reqs progress to specify _what_ the system must do & _how_ it must
  do it, effectively becoming a binding contract

there are also two main perspectives from which requirements are written:

- **user requirements** &mdash; high-level statements in natural language
  describing functionality & performance expected by the user; the book
  uses the Mentcare mental health system as a running example throughout
  ch. 4
- **system requirements** &mdash; precise, detailed specifications of what
  is to be implemented; intended for developers & testers rather than
  end users

### types of requirements

three broad types covered in the slides & book:

- _**functional requirements**_ &mdash; describe what the system should do,
  how it reacts to particular inputs, how it behaves in specific situations.
  functional reqs must be both _complete_ (covering all needed behavior) &
  _consistent_ (no conflicts between them); in practice, large systems make
  this very hard to achieve perfectly.
- _**non-functional requirements (NFRs)**_ &mdash; constraints on services or
  functions; often apply to the system as a whole rather than individual
  features. examples: performance, security, availability. the book emphasizes
  that NFRs are often _more_ critical than functional ones &mdash; if a NFR
  isn't met, the whole system may be unusable even if every functional req is
  implemented.
- _**domain requirements**_ &mdash; derived from the application domain itself,
  not from stated user needs. sw engineers may not fully understand them, which
  makes them tricky; domain experts need to be closely involved.

### types of non-functional requirements

the book & slides break NFRs into three sub-categories:

- **product requirements** &mdash; execution speed, memory, acceptable failure
  rate, portability, usability
- **organizational requirements** &mdash; policies & procedures, process
  standards, choice of programming language, methodologies & tools, delivery
  timeframe
- **external requirements** &mdash; interoperability w/ other systems, legal
  requirements, ethical requirements

> [!NOTE]
>
> NFRs can generate further functional requirements when worked out in detail.
> e.g., a security NFR might require adding an audit-log feature that becomes
> its own functional req.

## user req challenges

human language is messy, & that creates real problems for capturing user
requirements cleanly. three main challenges:

- _**ambiguity**_ &mdash; clarity is hard; brevity is also desirable; human
  language ≠ user language ≠ system language. what a user means & what a dev
  reads can be very different things.
- _**confusion**_ &mdash; functional vs. non-functional vs. system goals vs.
  design information get conflated; stakeholders aren't always sure where to
  capture which kind of information.
- _**amalgamation**_ &mdash; a single stated requirement may actually contain
  several requirements bundled together; this makes it hard to test, trace, &
  manage change later.

## capturing reqs: H-H-I

the slide frames requirements gathering as a _human-human interaction (H-H-I)_
problem between users & engineers. because it's fundamentally a communication
challenge, the following practices help:

- establish a standard format & stick to it
- use language consistently: **"shall"** = mandatory; **"should"** = desirable
- highlight key elements (bold, italic, etc.) to draw attention to
  critical constraints
- resist the temptation to use technical jargon &mdash; users don't speak
  developer language

the book adds that this interaction is complicated by:

- stakeholders not always knowing what they want
- a terminology gap between users & engineers
- conflicting needs from different stakeholder groups
- lack of "ownership" leading to politically-swayed requirements
- the simple fact that requirements _change_

## system req challenges

moving from user reqs to system reqs introduces its own set of problems:

- some design or implementation language may be necessary (e.g., specifying
  architecture, or interoperability constraints w/ existing infrastructure)
- natural language is inherently ambiguous &mdash; the same sentence can mean
  different things to different readers
- natural language allows saying the same thing multiple ways, making it hard
  to detect duplicates or conflicts
- relating related requirements to each other is difficult without dedicated
  tooling

## specification notations

several options for capturing requirements more precisely than plain natural
language:

- _**structured natural language**_ with standard forms/templates &mdash; most
  common in practice; reduces ambiguity while staying readable by non-technical
  stakeholders
- _**design description languages**_ (pseudo-code) &mdash; more formal;
  bridges the gap between reqs & implementation
- _**graphical notations**_ &mdash; use-case diagrams, sequence diagrams; very
  useful for visualizing interactions

> [!TODO]
>
> add use-case diagram example from slides here

> [!TODO]
>
> add sequence diagram example from slides here

- _**mathematical specifications**_ &mdash; finite-state machines or set
  notation; extremely precise but requires specialized knowledge; used mainly
  for critical/safety systems

## interface specification

clearly defining boundaries between system components is a key part of requirements:

- _procedural interfaces_ (APIs) &mdash; what functions/methods are exposed
  & how they're called
- _data structures_ &mdash; the format & type of information passed between
  components
- _representations for existing subsystems_ &mdash; when integrating w/ legacy
  or third-party systems, specifying the interface is critical to avoiding
  mismatches

## the requirements document

the _**software requirements specification (SRS)**_ is the formal output of the
requirements engineering process. the book outlines a standard structure:

1. preface
2. introduction
3. glossary
4. user requirements definition
5. system architecture
6. system requirements specification
7. system models
8. system evolution
9. appendices
10. index

this document serves both as a contract & as a reference throughout development,
testing, & maintenance.

## requirements engineering process

the overall process has the goal of creating & maintaining the system
requirements document. it proceeds through several steps, each producing
its own output:

| step | output |
|---|---|
| feasibility study | feasibility report |
| elicitation & analysis | system models |
| specification | user & system requirements |
| validation | requirements document |

### feasibility studies

before committing to a project, the team needs to answer:

- should we build it at all?
- are we _capable_ of building it?
- can we _become_ capable if not?
- will it integrate w/ existing systems?
- will we be able to maintain it after delivery?

this is a critical gate &mdash; it's much cheaper to decide _not_ to build
something before starting than to discover mid-project that it's infeasible.

### elicitation & analysis

working w/ stakeholders to _discover_ requirements is harder than it sounds.
challenges include:

- stakeholders don't always know what they want
- there's a terminology gap between users & engineers
- different stakeholder groups have conflicting needs
- lack of clear "ownership" leads to politically-swayed reqs
- requirements change during the project

the discovery process involves:

1. _discovery_ &mdash; actively finding out what stakeholders need
2. _classification & organization_ &mdash; grouping related reqs & structuring them
3. _prioritization & negotiation_ &mdash; resolving conflicts; deciding what's in scope
4. _documentation_ &mdash; writing it all down in a consistent format

### requirements discovery

multiple viewpoints should be considered:

- **interactor** viewpoints &mdash; people who interact directly w/ the system
- **indirect** viewpoints &mdash; influencers who don't interact directly but are
  affected (e.g., managers, regulatory bodies)
- **domain** viewpoints &mdash; standards & constraints from the application domain

techniques for discovery include:

- **interviewing** stakeholders (structured or unstructured)
- **capturing scenarios** &mdash; real-life stories of how users accomplish goals;
  these make abstract reqs concrete & testable
- **use-cases** &mdash; describing typical user interactions w/ the system; the
  basis for use-case diagrams

### ethnography

_**ethnography**_ is an observational technique borrowed from social science. the
idea is to watch people work in their actual environment rather than just asking
them about it. this matters because:

- what people _say_ they do & what they _actually_ do are often different
- it's effective at discovering requirements from actual work (not just how work
  is "supposed" to happen)
- it surfaces requirements derived from cooperation & awareness of co-stakeholder
  activities &mdash; things people do automatically that they'd never think to
  mention in an interview

## requirements validation

validation is a checkpoint that ensures the requirements define the system the
customer actually wants. things to look for:

- _**validity**_ &mdash; are the requirements necessary & sufficient?
- _**consistency**_ &mdash; are there conflicts between requirements?
- _**completeness**_ &mdash; are all stakeholder needs covered?
- _**realism**_ &mdash; are the requirements feasible given budget, tech, & time?
- _**verifiability**_ &mdash; can each requirement be tested?

> [!NOTE]
>
> requirements change is inevitable. requirements management after the initial
> document is created involves identifying & storing requirements, managing
> changes as they come in, & tracing relationships between requirements so
> the impact of a change can be assessed. this is where dedicated requirements
> management tooling starts to become worth the overhead.
