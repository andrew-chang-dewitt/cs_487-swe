---
title: "SWE: Proactive & Reactive QA"
description: "Week 4 lecture notes covering software testing & quality management — inspections, testing strategies, configuration management, & release management."
keywords:
  - "quality assurance"
  - "quality control"
  - "software testing"
  - "configuration management"
  - "test-driven development"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-02-03T11:25-06:00"
---

## agenda

- quality defined
- QA vs. QC
- quality goals & value
- planning for quality
- defect classification
- the role of testing (V&V)
- inspections
- development testing
  - unit testing
  - component testing
  - system testing
- test-driven development (TDD)
- release testing
- user testing
- test cases
- configuration management
  - change management
  - version management
  - system building
  - release management

## quality defined

_**quality**_ is the degree to which a project fulfills its requirements &mdash; a
degree of excellence. the slides call it a "critical yet understated requirement,"
which i thought was a nice way to put it: quality is itself a req that often
doesn't get written down explicitly.

_**quality management**_ then is the activity of creating policies & procedures &
enforcing compliance w/ project requirements to achieve that degree of excellence.

the book (ch. 24) frames this more broadly as an organizational concern: quality
management means establishing processes for ensuring products meet required
standards, then monitoring & improving those processes continuously.

### cleanroom sw development

worth mentioning as an extreme point on the quality spectrum: the _cleanroom_
approach targets zero-defect software by keeping the dev environment "ultra clean."
key characteristics:

- formally specify the system (state transitions)
- incremental development w/ user involvement
- structured programming; limit control & data abstraction
- rigorous sw inspections
- statistical testing for reliability

a good benchmark for what "taking quality seriously" looks like pushed to its
logical conclusion.

## QA vs. QC

these two terms get conflated a lot, but they're meaningfully different:

- _**quality assurance (QA)**_ &mdash; _prevent_ defects; improve quality through
  efficient activities throughout the entire sw life cycle; process-focused
- _**quality control (QC)**_ &mdash; _eliminate_ defective products; improve the
  rate of acceptable product delivery through defect detection, primarily late
  in the life cycle; product-focused

the distinction matters because QA is proactive (hence the title of this lecture)
while QC is reactive. both are necessary, but investing only in QC means you're
always playing catch-up w/ defects instead of designing them out.

### quality goals

what does the QA function actually try to do?

- prevent, discover, & eliminate defects
- deliver customer satisfaction
- enforce standards & process
- "mind the gate" (checkpoint-driven milestones)
- improve processes over time
- review, audit, monitor, verify, validate, & inspect

## the value of quality

why should an organization care? a few practical reasons from the slides:

- quality increases customer satisfaction; credibility attracts new business
- lack of quality leads to _rework_ &mdash; unscheduled work = unplanned
  expense + slipping schedules; working under duress increases likelihood of
  introducing more mistakes
- uptime & performance are largely determined by quality

the QA environment isn't simple, either. teams have to manage:

- contractual conditions (scope, time, budget)
- customer-supplier relationships (change management, acceptance)
- teamwork across varied skills & parallel activities
- supporting multiple projects simultaneously
- HCI/usability concerns
- turnover management (people leave; knowledge has to transfer)
- ongoing maintenance (enhancement, release management, troubleshooting)

## defect classification

understanding _what kinds of defects_ exist helps teams target prevention
efforts. common categories:

- incorrect specification of requirements
- misunderstanding of client's needs
- deviation from requirements (gold-plating or short-cutting)
- design errors
- implementation errors
- violation of standards
- poor test coverage
- user interface/usability errors
- documentation errors

> [!NOTE]
>
> the book notes that static analysis & inspections can find 60–90% of
> defects, while testing alone typically finds fewer. this is a strong
> argument for investing in inspections early rather than relying solely
> on test runs.

## planning for quality

quality doesn't happen by accident; it has to be planned:

- define checkpoints that support milestones
- use independent verification at critical points
- adopt a build-test-fix-retest loop
- make quality measurable & testable (if you can't measure it, you can't
  manage it)
- inspire high-quality deliverables: establish goals, obtain commitment,
  motivate performance
- collect data over time to drive improvement

### performing quality control

QC feedback loops work like this:

1. measure output
2. compare to expected
3. understand the gap
4. use that knowledge to improve

tools that help:

- _**root-cause analysis**_ &mdash; ask what caused a problem, then what caused
  _that_ cause, & keep going until you reach a systemic root; don't just fix
  symptoms
- _**histograms & Pareto charts**_ &mdash; the Pareto principle says ~80% of
  problems come from ~20% of causes; invest in eliminating the most problematic
  causes first to get the best return

> [!TODO]
>
> add Pareto chart example from slides here

### focus & culture

quality improvement requires commitment as part of organizational culture, not
just a QA team siloed off from dev. common improvement frameworks:

- _process maturity models_ &mdash; Six Sigma (targets 3.4 defects per million
  opportunities); CMMI (5 maturity levels from initial/chaotic to optimizing)
- _the agile approach_ &mdash; iterative, short feedback loops inherently
  support quality improvement

## the role of testing: V&V

testing sits under the broader umbrella of _verification & validation_:

- _**validation**_ &mdash; building the _right_ product (does it meet user needs?)
- _**verification**_ &mdash; building it _right_ (does it meet the spec?)

goals of testing:

- demonstrate correctness & completeness; at least one test per requirement
- discover defects

> [!WARNING]
>
> testing can only _show the presence_ of bugs, not their absence. no amount
> of passing tests proves a system is bug-free; it just raises confidence.

### fit for purpose

the book introduces "fit for purpose" as a pragmatic framing of quality:

- _sw purpose_: the more critical the system, the higher the required reliability
- _user expectations_: what defect rate is the user willing to tolerate? how
  much do they value the system's capabilities?
- _marketing environment_: competition drives quality decisions; sometimes
  "good enough now" beats "perfect later"

## inspections

_**inspections**_ are a static V&V technique &mdash; reviewing "readable"
representations like source code or design docs without executing the code.

key properties:

- not contingent on the code being executable; can catch defects very early
- inspected for adherence to specification & standards
- can assess portability, maintainability, & efficiency in ways that runtime
  testing cannot

inspections vs. testing:

- in testing, defects can _hide beneath_ other defects (a bug that crashes early
  prevents you from seeing bugs that come later)
- inspections expose the whole artifact at once; every line is scrutinized
  regardless of execution paths

the book adds that _program walkthroughs_ are a lighter-weight variant of formal
code inspections; both fall under the software reviews umbrella.

## development testing

done local to the development effort; three levels:

### unit testing

testing individual _logical units_ &mdash; functions, methods, classes &mdash; in
isolation. effective unit tests:

- cover normal behavior & abnormal/edge cases
- use realistic data
- test boundary conditions explicitly

### component testing

testing _interacting entities_ (objects, modules, subsystems) together. the
focus shifts from individual behavior to how components communicate & integrate.

### system testing

testing the system as a whole:

- proper operation under expected conditions
- exception handling (what happens when things go wrong?)
- load tolerance (does it hold up under realistic or peak load?)

> [!TODO]
>
> add diagram of testing pyramid from slides / book here

## test-driven development (TDD)

TDD _interleaves_ testing & code development rather than treating testing as a
separate phase:

1. write a failing test for the behavior you want
2. write the minimum code to make it pass
3. refactor while keeping tests green

benefits the slides & book both emphasize:

- forces _partitioning_ &mdash; you have to think clearly about units of behavior
  before writing code
- ensures _clean code_ &mdash; only code that passes tests gets added
- produces _automated regression tests_ as a side effect
- builds deeper understanding of the problem
- tests serve as _living documentation_

> [!NOTE]
>
> TDD needs occasional "big picture" assessment &mdash; writing test-by-test
> can lead to locally correct but globally incoherent design if you lose
> sight of the system architecture.

## release testing

establishes a "fit for use" version of the sw. different from development testing:

- done by an _independent_ team (not the developers who wrote the code)
- focus is on _validation_ (does it meet user needs?) rather than defect discovery
- usually _black-box_: testers don't need to see the source code

three main approaches:

- _**requirements testing**_ &mdash; trace each requirement to at least one test;
  confirm the system satisfies the spec
- _**scenario testing**_ &mdash; construct realistic user scenarios & run the
  system through them end-to-end
- _**performance/load testing**_ &mdash; verify that the system meets NFRs around
  speed, throughput, & stability under load

## user testing

the _**user acceptance test (UAT)**_ is the ultimate gate:

- _**alpha testing**_ &mdash; done within the development organization; simulated
  or real users exercise the system in a controlled setting
- _**beta testing**_ &mdash; a preliminary release goes out to a field of real
  users; feedback informs final fixes
- _**acceptance testing**_ &mdash; users (or their designated representatives)
  formally determine whether the system is "fit" for deployment

## test cases

good test cases balance two goals:

- _**effectiveness**_ &mdash; efficiently discover defects; credibly demonstrate
  proper operation
- _**efficiency**_ &mdash; repeatable, self-documenting, easy to develop & maintain

strategies for writing good test cases:

- test _normal_ AND _abnormal_ inputs
- use realistic data (not just happy-path values)
- test boundaries explicitly &mdash; off-by-one errors are a classic source of bugs

## configuration management

_**configuration management (CM)**_ supports the evolution of a sw system through
a progression of versions. it's the infrastructure that makes controlled change
possible. four main CM activities:

### change management

change happens &mdash; mainly for good reasons. the challenge is managing it
without introducing chaos:

- _change requests_ &mdash; formalizing change reduces risk (though too much
  formality dampens the rate of change; a balance is needed)
- _impact assessment_ &mdash; before approving a change, understand what it
  affects
- _Change Control Board (CCB)_ &mdash; a designated decision-making body for
  approving/rejecting changes
- _implementation_ &mdash; planning, timing, cutover, & rollback procedures

### version management

keeping track of what version of what is where:

- version & release identification (tagging, numbering schemes)
- storage management & tracking change history
- the classic checkout–modify–check-in workflow (familiar from git)
- _branching_ &mdash; parallel development of features or fixes
- _merging_ &mdash; bringing parallel changes back together
- _baselines_ &mdash; a fixed snapshot of the system at a known-good state

> [!TODO]
>
> add branching & merging diagram from slides here

### system building

compiling & linking the latest checked-in components into a runnable version:

- build script generation
- VM/container integration
- minimal recompilation (only rebuild what changed)
- executable creation
- test automation integration

modern CI/CD pipelines are essentially automated system builds triggered by
every commit.

> [!TODO]
>
> add continuous integration pipeline diagram from slides here

### release management

two kinds of releases (from the slides):

- _**major releases**_ &mdash; significant new functionality; new version number
- _**minor releases**_ &mdash; patches & bug fixes; incremented sub-version number

release planning has to account for:

- current quality state of the product
- platform changes (OS upgrades, API deprecations, etc.)
- competitive landscape
- marketing commitments
- custom changes for specific customers

> [!NOTE]
>
> the book ties CM back to quality management: without disciplined CM,
> even well-tested code can be undermined by uncontrolled changes slipping
> into production. version control (git, etc.), build pipelines, & release
> management processes are the practical implementation of CM in most
> modern teams.
