---
title: "SWE: Software Evolution & Resilience"
description: "Week 9 lecture notes covering sw evolution dynamics, reengineering, refactoring, legacy systems, resilience engineering, & cybersecurity."
keywords:
  - "software evolution"
  - "resilience engineering"
  - "legacy systems"
  - "refactoring"
  - "reengineering"
  - "cybersecurity"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-03-10T11:25-06:00"
---

## agenda

- sw evolution: why change is inevitable
- evolution dynamics (Lehman's laws)
- managed change processes
- maintenance & its drivers
- reengineering & refactoring
- legacy systems: options & assessment
- sociotechnical systems
- resilience: the 4 R's
- cybersecurity controls

## sw evolution: managing inevitable change

continuing from the [previous lecture](./0224-artificially_intelligent_systems.md),
which covered AI & safety-critical systems, we now turn to what happens _after_
sw is deployed: it must evolve or die.

sw doesn't exist in a vacuum. business needs shift, technology advances, users
discover what they actually wanted (vs. what they asked for). the cycle is:

**evolve → release → evolve → release → ...**

reasons sw must change:

- support & facilitate business growth
- take advantage of technology innovation
- correct defects discovered in production
- adapt to new regulatory or security requirements

## evolution dynamics (Lehman's laws)

Lehman's laws of sw evolution describe patterns observed across many long-lived
systems. key takeaways:

- _**continuing change**_ &mdash; sw used in a real-world environment must be
  continuously adapted or it becomes progressively less satisfactory
- _**increasing complexity**_ &mdash; as sw evolves, structure degrades; adding
  to existing structure introduces instability; new functionality may bring new
  defects
- _**self-regulation**_ &mdash; sw evolution is largely self-regulating; metrics
  like size & defect rates remain roughly stable over release cycles
- _**conservation of organizational stability**_ &mdash; average effective global
  activity rate stays constant over time; orgs have limited capacity for change
- _**conservation of familiarity**_ &mdash; devs must maintain understanding of
  the codebase; adding too much at once violates this & increases risk

### what happens if you don't evolve?

systems either grow or progressively lose value — user satisfaction drops,
perceived quality declines. stagnation is not neutral. but uncontrolled growth
is also dangerous:

- evolution tends to _increase complexity_
- bigger systems tend to _resist_ evolution
- organizational bureaucracy _dampens_ evolution further
- bigger the change, the greater the number of associated problems

## managed change

change is inevitable — but _unmanaged_ change is dangerous. a structured process:

1. _**formal change requests/proposals**_ — purpose & priority; cost & effort;
   risk assessment attached to every request
2. _**change review & authorization**_ — a _change control board_ (CCB) evaluates
   requests; balances value against risk & resource cost
3. _**change implementation**_ — standard sw engineering practices; planning &
   project management apply
4. _**change release**_ — communication to stakeholders; rollback planning in case
   the release causes new problems

the CCB is the organizational mechanism that prevents "let's just fix it quick"
from becoming "we just destabilized production."

## maintenance

development effort & discipline _should_ reduce maintenance effort downstream:

- better analysis → better alignment w/ user needs → fewer change requests
- better design/implementation → fewer defects → less corrective maintenance
- more thorough QA → fewer production defects → less emergency patching

> [!NOTE]
>
> an evolutionary (agile) approach can paradoxically _increase_ maintenance
> costs if discipline slips — cutting corners on each sprint accumulates
> technical debt that eventually must be paid. change should always be managed
> w/ discipline: defect removal _and_ enhancements both require rigor.

### drivers of maintenance activity

factors that predict high maintenance burden:

- _**interfaces**_ — number & complexity; both user-facing & system-to-system;
  every interface is a change surface
- _**information**_ — number of data sources; data structure complexity; schema
  changes are expensive
- _**volatile requirements**_ — policies/procedures, business rules, technology
  platforms all shift; systems tied to volatile reqs are high-maintenance
- _**processes utilizing the system**_ — more users = more demand for change;
  wider user base amplifies every imperfection

## reengineering & refactoring

### reengineering

reengineering creates a newer, more maintainable version of an existing system
without fundamentally changing its functionality. benefits:

- faster & cheaper than building brand-new from scratch
- preserves domain knowledge embedded in the existing system
- reduces risk of catastrophic cutover failures

process typically includes:

- _reverse engineering_ — understanding the existing system well enough to
  produce a higher-level description of what it does
- _restructuring_ — transforming the structure (code, data, architecture) to
  improve maintainability
- _forward engineering_ — using the higher-level understanding to produce an
  improved implementation

### refactoring

refactoring is _preventive maintenance_ — touching up the codebase regularly
to stave off structural degradation before it becomes a crisis. key distinction:

> improve what's already there — **don't add new functionality**

refactoring targets:

- _removal of duplicate code_ — DRY; two copies means two places to fix bugs
- _decomposing long methods_ — long methods hide complexity & resist testing
- _simplify or replace switch statements_ — often a sign of missing polymorphism
- _encapsulate recurring "clumps" of data_ — if you always pass the same 4
  variables together, they should be an object
- _remove speculative generality_ — delete abstractions added "just in case";
  YAGNI (you ain't gonna need it)

## legacy systems

systems supporting critical business functions often _hang around for decades_:

- change is risky — broken dependencies everywhere
- need downtime to switch — some systems can't afford downtime
- domain knowledge seeps away — the people who understood why it works like
  that have retired or left

### options

- _**scrap it**_ — when business value is gone; often the right call but
  politically difficult
- _**leave as-is & maintain**_ — if it ain't broke... but technical debt
  accumulates
- _**reengineer**_ — improve maintainability without full replacement
- _**replace all or part**_ — highest risk, highest reward; often done
  incrementally (strangler fig pattern)

### assessment framework

assess on two dimensions:

- _**business value**_ — how critical is this system to current operations?
- _**system quality**_ — how maintainable, stable, & understandable is it?

> [!TODO]
>
> add 2×2 matrix diagram (slide 13): business value (low/high) vs. system
> quality (low/high) showing recommended action for each quadrant here

high value + high quality → maintain carefully.
high value + low quality → reengineer (priority).
low value + high quality → consider replacement w/ something modern.
low value + low quality → scrap it.

## sociotechnical systems

sw doesn't exist in isolation — it's embedded in a _sociotechnical system_
that includes hardware, people, processes, & organizational context.

the sociotechnical stack (bottom to top):

1. _equipment_ — physical hw
2. _operating system_ — platform layer
3. _communications & data management_ — middleware, databases
4. _application_ — the sw we typically think about
5. _business process_ — how work actually gets done using the system
6. _organizational_ — policies, governance, structure
7. _social_ — culture, incentives, human behavior

implications for evolution: changing the _application_ layer doesn't mean the
system has changed. if business processes & organizational behaviors don't
adapt, sw changes may fail to deliver value — or may actively disrupt operations.

## resilience engineering

### what is resilience?

_**resilience**_ &mdash; the ability of a system to withstand stress to the
point of complete recovery. specifically for sw systems:

> resiliency = ability to continue to provide services as specified, even under
> stress of disruptive events (equipment failures, user errors, cyberattacks)

key shift from traditional reliability thinking: _failure happens — design to
handle it_, not just to prevent it. reliability focuses on preventing failure;
resilience _accepts that failures will occur_ & focuses on recovery.

implied: _critical services_ have priority. not all services need to be equally
resilient — triage matters.

extension: resilience also applies to _change_ — a resilient system can adapt
to unexpected evolution without collapse.

### the 4 R's of resilient activities

_**recognition**_ &mdash; maintain adequate situational awareness to detect
that something is wrong. you can't respond to what you haven't noticed.

_**resistance**_ &mdash; early detection may allow "fighting off" the
disruptive condition before it fully impacts the system. rate-limiting, circuit
breakers, input validation.

_**recovery**_ &mdash; timely restoration of (especially critical) systems to
minimize disruption. backup systems, failover, rollback procedures.

_**reinstatement**_ &mdash; return to full normal operation after the incident.
root cause analysis; prevent recurrence; restore full capability (not just
limp-mode operation).

### resilient design approaches

- _**layered protection (defense in depth)**_ — multiple overlapping controls;
  no single layer assumed to be sufficient
- _**fail-safe design**_ — when the system fails, it fails into a _safe_ state
  (not an open or destructive one)
- _**self-monitoring**_ — system detects its own anomalies; watchdog timers,
  health checks, automated alerts
- _**redundancy**_ — duplicate critical components so single failures don't
  bring down the whole system; geographic distribution for disaster resilience
- _**recovery mechanisms**_ — planned & tested runbooks for restoring service;
  chaos engineering to validate recovery before a real crisis

## cybersecurity

our massively interconnected environment offers many paths for opportunistic
attackers. cybersecurity is increasingly a _non-functional requirement_ — not
optional, not an afterthought.

### security controls

_**authentication**_ &mdash; forcing users to prove they are authorized to
access assets. multi-factor auth raises the bar significantly.

_**encryption**_ &mdash; altering the form of sensitive data so unauthorized
users can't understand or use it even if they obtain it. at rest & in transit.

_**firewalls**_ &mdash; protective checkpoints for restricting traffic flow to
only trusted sources. network-layer, application-layer (WAF), & host-based.

> [!NOTE]
>
> these controls map directly to the resilience framework: authentication &
> firewalls support _resistance_; encryption limits damage when resistance
> fails (limiting impact of a breach). detection systems (IDS/IPS) support
> _recognition_. incident response plans support _recovery_ & _reinstatement_.

### cybersecurity & the sociotechnical stack

security controls at the technical layer are necessary but not sufficient. the
social & organizational layers matter just as much:

- users who choose weak passwords or click phishing links defeat technical
  controls
- organizations that don't train staff on security procedures create
  exploitable gaps
- governance that doesn't treat security as a priority doesn't fund adequate
  controls

a resilient cybersecurity posture addresses all layers of the sociotechnical
stack — not just the technical ones.

> [!TODO]
>
> add diagram of the resilience/cybersecurity overlap from ch. 14 here
