---
title: "SWE: Risk & Exception Management"
description: "Week 6 lecture notes covering proactive risk management, exception handling, dependability, reliability engineering, & secure design."
keywords:
  - "risk management"
  - "exception handling"
  - "dependability"
  - "reliability engineering"
  - "security"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-02-17T11:25-06:00"
---

## agenda

- risk management
  - exposure assessment
  - mitigation analysis & choices
- exception management
  - detection engineering
  - handling strategies
- failure categories
- dependability considerations
- specification for dependable systems
- safety-critical systems
- security: the need & key concepts
- security management
- designing for security
- dependable programming practices
- risky programming constructs
- survivability

## risk management

picking up from the [previous lecture](./0210-modeling_and_design.md) on
modeling & architecture, this week we zoom into a specific design concern:
what _threatens_ the system's success, and how do we deal with it?

_**risk**_ &mdash; a threat to success that must be managed _proactively_,
not just reacted to after the fact. the word "proactively" is doing a lot of
work here. the whole point of risk management is that you do the hard thinking
_before_ something goes wrong.

### exposure assessment

the process starts with understanding what you actually have to lose:

1. _identify assets_ &mdash; what needs protection? this includes not just
   sw artifacts but data, business processes, reputation, & user safety
2. _identify threats_ &mdash; what could go wrong? who or what might cause it?
3. _assess likelihood_ &mdash; probability of each threat actually occurring
4. _assess impact_ &mdash; cost (in dollars, time, safety, or otherwise) if
   the threat materializes
5. _calculate exposure_ &mdash; `Likelihood(%) × Impact($)` gives you a
   comparable number across threats; prioritize by exposure

### mitigation analysis

once you know your exposure, you evaluate options for reducing it:

- _identify mitigations_ &mdash; what could you do to reduce likelihood or
  impact?
- _estimate cost_ of each mitigation
- _assess benefit_ &mdash; how much does this mitigation reduce exposure?
- _decide_ &mdash; mitigate if benefit > cost; don't if cost > benefit

### mitigation choices

four possible outcomes after the analysis:

- _**implement mitigation**_ &mdash; benefit exceeds cost; do it
- _**proceed without mitigating**_ &mdash; either all mitigations are
  infeasible (cost > benefit for all options) _or_ the remaining exposure is
  acceptably low
- _**cancel the project**_ &mdash; all mitigations infeasible & exposure
  unacceptably high; the honest but rare conclusion
- _**deep analysis as mitigation**_ &mdash; even if you don't implement a
  technical mitigation, thorough risk analysis itself reduces exposure by
  increasing understanding; you know where the landmines are

## exception management

_**exceptions**_ &mdash; deviations from expected runtime behavior. different
from design-time risk: exceptions happen _while the system is running_.

### detection engineering

you can't handle what you can't detect. detection involves:

- _sensing_ &mdash; monitoring system state for deviations
- _lookup table of expected exceptions_ &mdash; catalog known exceptional
  states so the system can recognize them
- _the hard question_: what if an unexpected event occurs that isn't in the
  lookup table? the system may not even know it's in an exceptional state.
  this is where "imagineering" comes in — trying to imagine ahead of time all
  the ways things could go wrong.

### handling strategies

once an exception is detected:

- _goal_ &mdash; get back to "normal" ASAP
- _alternate execution path_ &mdash; follow the pre-planned recovery path
- _catch-all handlers_ &mdash; when specific handling isn't possible, aim for
  a "safe" state rather than crashing
- _lag times_ &mdash; delay between detection & handling threatens recovery;
  time is usually of the essence
- _"imagineering"_ &mdash; the slides use this term for the practice of
  imaginatively working through failure scenarios to design handlers in advance

> [!NOTE]
>
> the book (ch. 11) distinguishes between _fault avoidance_ (don't introduce
> faults in the first place), _fault detection/correction_ (find & fix faults
> before they cause failures), & _fault tolerance_ (keep working even when
> faults occur). exception handling primarily lives in the fault tolerance
> category.

## failure categories

three root causes of system failures:

- _**hardware failure**_ &mdash; design errors in hw, or component failure
  over time
- _**software failure**_ &mdash; requirements issues (built the wrong thing),
  design errors, or coding defects
- _**operational failure**_ &mdash; user misuse; the system does exactly what
  it was designed to do, but the user does something it wasn't designed for

## dependability

_**dependability**_ is the umbrella term for properties that make a system
trustworthy in operation. key dimensions (from ch. 10):

- _**availability**_ &mdash; probability the system is up & accessible when
  needed
- _**reliability**_ &mdash; probability of delivering correct service over a
  given time period
- _**safety**_ &mdash; system won't harm users or the environment even when
  it fails
- _**security**_ &mdash; system resists malicious attack
- _**resilience**_ &mdash; system can recover from failures & attacks

### dependability considerations from the slides

- _**repairability**_ &mdash; ability to recover from failure; includes
  diagnosis, analysis, & targeted ("surgical") repair
- _**maintainability**_ &mdash; economical adaptation to new or changed reqs
- _**survivability**_ &mdash; ability to withstand attack; recognize it,
  resist it, & recover from it
- _**error tolerance**_ &mdash; avoid or tolerate user errors; autocorrect
  where possible; educate the user as a last resort

### dependability costs money

adding fault tolerance is expensive. you can't just make everything maximally
dependable — that's not economically feasible. cost-benefit analysis applies:
how critical is this system? how much would a failure cost? spend accordingly.

key techniques for achieving dependability:

- _**redundancy**_ &mdash; hw redundancy for fault tolerance; sw redundancy
  (N-version programming: multiple independent implementations of the same
  spec run in parallel; vote on the result)
- _**diversity**_ &mdash; using _different_ implementations to avoid
  common-mode failures (if two implementations were written differently, they're
  unlikely to fail on the same input)
- _**dependable processes**_ &mdash; formal methods, rigorous inspections,
  structured testing; process discipline is itself a dependability mechanism

## specification for dependable systems

formal specification approaches:

- _**risk-driven**_ &mdash; focus the spec on avoiding identified hazards
- _**reliability**_ &mdash; measurable performance standards (how often can
  this fail? under what conditions?)
- _**security**_ &mdash; authorization requirements & protection policies
- _**formal specification**_ &mdash; human communication is inherently
  error-prone; formality (mathematical notation, model checking) seeks to
  reduce ambiguity; but the slides note it has _limited effectiveness in
  practice_ because writing formal specs is expensive & hard to validate
  w/ stakeholders

## safety-critical systems

two categories:

- _**primary safety-critical**_ &mdash; embedded system controllers where
  failure of the controller _directly_ leads to system failure, injury, or
  environmental damage (think aircraft flight controls, insulin pumps)
- _**secondary safety-critical**_ &mdash; sw that doesn't directly control
  safety-critical hw, but whose failure _could lead to_ harmful situations
  (e.g., a defective CAD or CASE tool that produces flawed designs)

## the need for security

openness has genuine benefits — data sharing, remote user access, integration
with partner systems. but openness introduces vulnerabilities:

- unauthorized access
- denial of service
- exposure of sensitive data
- data corruption

the slides draw a useful distinction:
- _application security_ &mdash; a **sw engineering** problem
- _infrastructure security_ &mdash; a **systems engineering** problem

both matter; they require different expertise.

### security concepts

- _**asset**_ &mdash; system resource that must be protected
- _**exposure**_ &mdash; potential loss or harm if an asset is compromised
- _**vulnerability**_ &mdash; an exploitable weakness in a system
- _**attack**_ &mdash; exploitation of a vulnerability
- _**threat**_ &mdash; circumstances under which an attack can occur
- _**control**_ &mdash; a protective measure that reduces vulnerability

### security management activities

- _**access management**_ &mdash; user & permission management; restrict
  what each user can see & do (principle of least privilege)
- _**deployment management**_ &mdash; control installation & configuration;
  patching & update management
- _**attack management**_ &mdash; monitoring, detection, & recovery

## designing for security

architectural-level security design:

- _protect critical assets_ &mdash; know what matters most & layer defenses
  around it
- _distribute assets_ &mdash; don't put all eggs in one basket; compartmentalize
  to minimize blast radius of a successful attack (the "medieval castle" analogy
  from the slides: multiple walls, not one big one)
- _establish & adhere to explicit policies_ &mdash; security by accident isn't
  security; write down the rules & follow them
- _minimize impact through redundancy, compartmentalization, & isolation_
- _design for recoverability_ &mdash; assume you will be attacked; plan for how
  to get back to normal
- _maintain usability_ &mdash; security controls that users route around aren't
  securing anything
- _validate all inputs_ &mdash; never trust data coming in from outside the
  system boundary

### designing for deployment

security doesn't stop at the code level; the deployment matters too:

- support viewing & analyzing configurations (so you know what's actually
  deployed)
- _minimize default privileges_ &mdash; principle of least privilege by default
- _localize configuration settings_ &mdash; make them easy to find & audit
- make it easy to fix vulnerabilities quickly (patch fast)

## dependable programming practices

at the code level, these habits reduce defect rates & improve dependability:

- control visibility of information (encapsulation; don't expose what doesn't
  need to be exposed)
- check _all_ inputs for validity — especially inputs from external sources
- handle _all_ exceptions — don't leave any code path w/o a handler
- avoid error-prone code constructs (see risky constructs below)
- provide recovery & restart capabilities
- check array bounds explicitly
- include timeouts when interfacing w/ external components (never wait forever)
- name all constants that represent real-world values (no magic numbers)

## risky programming constructs

the slides enumerate constructs that introduce disproportionate risk:

- _unconditional branching_ (go-to's) — destroys control flow traceability
- _floating point numbers_ — precision issues; never compare for equality
- _pointers_ — easy to corrupt memory; hard to audit
- _dynamic memory allocation_ — memory leaks, use-after-free, fragmentation
- _parallelism_ — race conditions, deadlocks, non-determinism
- _recursion_ — stack overflow; hard to reason about depth
- _interrupts_ — can fire at any time; hard to test all interleavings
- _inheritance_ — can obscure behavior; deep hierarchies are fragile
- _aliasing_ — multiple references to the same memory; changes in one place
  have unexpected effects elsewhere
- _unbounded arrays_ — buffer overflow vulnerabilities
- _default input processing_ — accepting anything the user sends; must validate

> [!WARNING]
>
> "risky" doesn't mean "never use." it means "use with extra care, more
> testing, & clear documentation." some of these (parallelism, dynamic
> allocation) are unavoidable in real systems. the point is to _know_
> where the danger is.

## reliability engineering

from ch. 11 of the book, a bit more quantitative view of dependability:

_**reliability**_ &mdash; the probability that a system delivers services
correctly over a given time period & under given conditions.

### reliability metrics

- _**ROCOF**_ (Rate Of OCcurrence Of Failures) &mdash; how often does the
  system fail?
- _**MTTF**_ (Mean Time To Failure) &mdash; on average, how long between
  failures?
- _**MTBF**_ (Mean Time Between Failures) &mdash; like MTTF but includes
  repair time; MTBF = MTTF + MTTR
- _**availability**_ &mdash; proportion of time the system is operational;
  `availability = MTTF / (MTTF + MTTR)`

these metrics turn "the system is reliable" from a vague claim into a
_testable, contractual commitment_.

### reliability achievement strategies

- _**fault avoidance**_ &mdash; write better code; use better processes;
  don't introduce faults in the first place
- _**fault detection & correction**_ &mdash; testing & inspections; find &
  fix faults before deployment
- _**fault tolerance**_ &mdash; design the system to keep working even when
  faults occur:
  - _protection system_ &mdash; monitors for failures & switches to backup
  - _self-monitoring multiprocessor_ &mdash; multiple processors check each
    other's outputs
  - _N-version programming_ &mdash; independent implementations; vote on result

### statistical testing & reliability growth

statistical testing is specifically designed for reliability _assessment_ (not
defect detection). you run the system against a statistically representative
sample of inputs from the operational profile & measure failure rates.

_**reliability growth models**_ predict how reliability will improve as testing
& fixes occur. useful for planning: "at this fix rate, when will we hit our
reliability target?"

## survivability

_**survivability**_ &mdash; the ability to fulfill a mission in the presence
of attacks or failures. three-part strategy:

- _**resistance**_ &mdash; prevent attacks from succeeding in the first place
- _**recognition**_ &mdash; detect that an attack is occurring or has occurred
- _**recovery**_ &mdash; maintain adequate operation during the attack, then
  restore full operation afterward

the key insight: you can't always _prevent_ attacks, but you can _design
systems that survive them_. resistance alone isn't a complete strategy.
