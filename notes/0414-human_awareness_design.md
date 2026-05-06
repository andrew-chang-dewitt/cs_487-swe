---
title: "SWE: Human Awareness Design"
description: "Week 13 lecture notes covering project management basics, situational awareness (SA), HCI design principles, complexity management, alarms, & automation."
keywords:
  - "situational awareness"
  - "human awareness design"
  - "project management"
  - "HCI"
  - "UCD"
  - "complexity"
  - "automation"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-04-14T11:25-06:00"
---

## agenda

- what is a project?
- objectives, constraints & scope triangle
- stakeholders & project definition
- work decomposition
- estimating sw development
- productivity
- human awareness defined
- mission-critical awareness examples
- situation awareness (SA) levels
- time lags & the awareness loop
- assessment elements & dashboards
- sources of uncertainty & managing it
- complexity: system, operational, apparent
- complexity design principles
- the role of alarms
- building better automation
- uninhabited vehicles

## project management (first half)

picking up from the [previous lecture](./0407-service_agentic_arch.md) on
service & agentic architectures, we now step back & look at the broader
management context in which swe happens — then pivot to the human awareness
design material that is the core theme of the week.

### what is a project?

_**project**_ &mdash; application of resources to produce a product / deliver
a service.

key characteristics:
- _temporary_ — definite beginning & ending
- _unique_ — never done exactly this way before
- _has objectives / requirements_

lifecycle:
- _begins_ when involved parties agree to objectives (contractual obligation)
- _ends_ when objectives (or agreed-upon revised set) are met — or determined
  to be unattainable

### objectives & constraints

- _objectives_ are desired results; they form the basis of project planning
- _constraints_ are restrictions primarily associated with parameters of the
  _scope triangle_

> [!TODO]
>
> add scope triangle diagram here — the classic time / cost / scope (quality)
> triangle; illustrate how changing one vertex forces changes to others

### stakeholders

_**stakeholder**_ &mdash; anyone impacted by the project &/or its outcome:
customer, sponsor, management, project team, partners.

- proactive communication is _critical_ to stakeholder satisfaction
- misaligned expectations are a leading cause of project failure

### the need for project definition

before planning, must answer:
- what will this project achieve?
- when will it complete?
- how many people w/ which skills?
- how much will it cost?

_consensus among stakeholders is critical to success._ definition must precede
planning — you can't plan toward an undefined goal.

### scope of work

- defines objectives & work to be produced
- begins as client request; negotiated into contract of deliverables
- must also define what _won't_ be done (scope exclusions matter)
- establishes key milestones & environmental requirements
- agree to _conditions of satisfaction_
- distinguish: _project scope_ (work to produce the product) vs. _product scope_
  (features & functions of the product)
- largely overlaps w/ sw engineering's requirements

### inter-related project parameters

what we can accomplish (scope) & how well (quality) are factors of:
- investment (cost)
- calendar time
- resource effort

> [!NOTE]
>
> a change to any one of these 5 factors (scope, quality, cost, time, effort)
> _forces_ a change to at least one of the other four. this is the iron law
> of the scope triangle. can't add features for free.

### managing project priorities

priorities determine which factors are:
- _constrained/fixed_ — non-negotiable; can't be changed
- _enhanced_ — optimized toward; target for improvement
- _accept/tolerate_ — slackened; allowed to degrade if necessary

must be negotiated to meet objectives while maintaining equilibrium of the
scope triangle.

### work decomposition

breaking the goal into manageable pieces.

decomposition techniques:
- _top-down_ — start from the goal, decompose into sub-goals; good for
  well-understood domains
- _bottom-up_ — start from known tasks, aggregate into larger units; useful
  when tasks are known but overall structure isn't
- _activities vs. deliverables_ — decompose by what you _do_ or what you
  _produce_; deliverable-based decomposition is often easier to track

stopping rules (when is a work package small enough?):
- progress/completion can be _measured_
- start/end events _clearly defined_
- effort can be _estimated confidently_
- required skills _well understood_

### estimating sw development

things to estimate: time, effort, cost, defects, user satisfaction

drivers (inputs to the estimate):
- requirements, objects, components, subsystems, interfaces, methods,
  data tables, complexity

cost elements:
- _labor_ — dominant cost in most sw projects
- _infrastructure_ — servers, cloud, networking, licenses
- _tools_ — IDEs, testing tools, CI/CD infrastructure
- _travel, training_ — often underestimated

estimation approaches:
- _algorithmic cost modeling_ (e.g., COCOMO) — formula-based; requires
  calibration to your organization's historical data
- _expert judgment_ — ask experienced engineers; fast but subjective
- _estimation by analogy_ — compare to similar past projects; requires
  good historical records
- _function point analysis_ — count functional units (inputs, outputs,
  queries, files, interfaces); language-independent measure of size

> [!NOTE]
>
> uncertainty decreases over time:
> feasibility → requirements → design → code → delivery.
> estimates made early are inherently less reliable. plan for re-estimation
> at each phase gate. communicate uncertainty ranges, not false precision.

### productivity

_productivity_ &mdash; N units produced / M person-hours.

possible numerators:
- _lines of code (SLOC)_ — easy to measure; problematic (more code isn't
  better; language-dependent)
- _function points_ — language-independent; more stable measure of functionality

factors affecting productivity:
- experience of the team
- process maturity
- project size (larger projects = lower productivity per person; coordination
  overhead grows)
- tool support
- working environment

## human awareness engineering (second half)

this is the core theme of the lecture. the first half (PM) provides the
organizational context; this half addresses the _human_ in the human-computer
interface.

### human awareness defined

_**awareness**_ &mdash; being aware of your environment: current state & what's
coming next. being able to extract _relevant_ information from the flow of data;
prioritizing correctly.

awareness is always assessed w/ respect to _specific goals of a particular job_.
generic "awareness" isn't useful — you need to be aware of the _right things_.

two categories of human partners:
- _directly interacting_ — users operating the system
- _indirectly affected_ — people impacted by the system's outputs/decisions
  without directly using it

### mission-critical awareness examples

- _a driver_: other vehicles/obstacles; speed & direction; rules & road conditions
- _a doctor treating a patient_: vital signs & symptoms; relevant patient
  history; "best practices"
- _an air traffic controller_: speed, direction, & altitude of all planes;
  weather conditions

> [!NOTE]
>
> each of these _could_ be automated. the question is whether it's worth it,
> & whether automation would actually achieve adequate SA — or just shift the
> burden to the automation system.

### the importance of awareness

- _improves decision making_: faster & better
- _prepares user for exceptions_: universe of possible exceptions is smaller
  & narrower when you know current state
- _facilitates appropriate automation_: "normal" is predictable & can be
  automated safely when users & systems share situational awareness

### situation awareness (SA) levels

_**situational awareness**_ &mdash; Mica Endsley's three-level model:

_**level 1 — perception**_: status, attributes, & dynamics of relevant
elements in the environment. the raw "what is happening right now?"

_**level 2 — comprehension**_: what does the data _mean_ in the context of
relevant goals & objectives? synthesizing level 1 data into understanding.

_**level 3 — projection**_: predicting future state; selecting next actions.
"if current trends continue, what will happen & what should I do?"

> [!TODO]
>
> add SA levels diagram here — showing the three levels stacked (perception
> → comprehension → projection) w/ feedback loops from the environment

each level depends on the one below it. you can't project (level 3) if you
haven't comprehended (level 2); you can't comprehend if you haven't perceived
(level 1).

### time lags

the path from unaware to acting:
level 1 (receive indication) → level 2 (process to recognize meaning) →
level 3 (assess proper response) → action

every step takes time:
- communication, processing, retrieval, assessment, & execution all introduce
  delay
- _total time lag_ = duration between event & return to normal (or at least safe)
- minimizing time lag is _highly desirable_
- beating "point of no return" is _required_ — miss that & no amount of awareness
  helps

making time lag _consistent & predictable_ allows for a complete engineered
solution (potentially automated).

### the awareness loop

> [!TODO]
>
> add awareness loop diagram here — entity A senses → analyzes → signals →
> entity B senses → analyzes → acknowledges; time to close the loop shown

key insight: _one entity can inspire awareness in a partner by sending a signal,
but the sender cannot guarantee the receiver actually becomes sufficiently aware._

to close the loop: receiver replies w/ acknowledgement of awareness.
time to close the loop should be included in total time lag calculations.

### assessment elements

factors that determine how quickly & reliably a user achieves SA:

- _time_ — how long to become situationally aware
- _perception & attention_ — humans have finite capacities for conscious &
  sub-conscious processing; can't attend to everything simultaneously
- _working memory_ — 7 ± 2 chunks in working memory at once; overloading it
  degrades comprehension
- _mental models_ — users organize experiences & analyze situations
  methodically; good design aligns w/ users' existing mental models
- _user goals_ — ultimately: "did I get my job done?"

### dashboards

_**dashboard**_ &mdash; information of all kinds consolidated into a single
display with high information density & rapid interpretability.

historical precedents: car dashboards; industrial control panels; cockpit
instrumentation. modern: business intelligence dashboards.

the pitch: "so simple a CEO can use it" — meaning high-level summary, not
raw data dump. the challenge is designing what goes _on_ the dashboard & how
it's represented.

## sources of uncertainty

SA is degraded by uncertainty. sources:

_level 1 (perception) uncertainty_:
- missing info — data not available
- reliability/credibility — is the sensor trustworthy?
- conflicting data — two sources disagree
- timeliness — data is stale
- noisy data — signal-to-noise ratio too low

_level 2 (comprehension) uncertainty_:
- challenging abstraction — hard to synthesize level 1 data into meaning

_level 3 (decision) uncertainty_:
- factor of uncertainty across all three levels compounds; hard to project
  confidently when perception & comprehension are uncertain

### managing uncertainty

users naturally work to remove uncertainty:
- rely on defaults
- accept "good enough" rather than waiting for perfection
- process of elimination

good design helps by:
- providing supplemental information
- representing critical info in _multiple ways_ (redundant representations)
- providing multiple sources
- supporting "bet-hedging" — helping users act under residual uncertainty

### support uncertainty management

design principles:
- make it easy for users to _assess reliability_ of displayed data
- _fewer, more distinct choices_ → more rapid decision making
- cues to assist should be _prominently presented proximally_ to the
  information they relate to

## complexity & SA

complexity inherently impedes SA. but complexity is _dynamic_:

- the more we learn about a complex environment, the simpler it becomes (for us)
- demand for more features increases complexity again

designers' goals:
- balance features & complexity
- help users learn
- expand feature set judiciously

### types of complexity

_**system complexity**_ &mdash; relatively objective; can be measured &
reduced measurably.

metrics:
- number of items (objects, functions, states)
- degree of interaction between items
- system dynamics (frequency of status change; predictability of changes)

_**operational complexity**_ &mdash; how difficult is the system to _use_?

- system complexity does _not_ imply operational complexity (cars are
  mechanically complex but operationally accessible for most adults)
- reducing operational complexity can offset system complexity
- automation can reduce operational complexity — but not always; sometimes
  automation adds new operational complexity (mode confusion in aircraft
  automation is a classic example)

_**apparent complexity**_ &mdash; relatively subjective; does the system _look_
complex?

a function of:
- _cognitive complexity_ — ease of mapping interface to operation; transparency
- _display complexity_ — density, grouping, visual hierarchy
- _task/response complexity_ — number of steps; branching; error recovery burden

### complexity design principles

- _resist feature creep_ — every added feature has a cost in complexity
- _manage feature groups_ (prioritize) — make important things prominent
- _be consistent_ — same action should produce same result everywhere
- _simplify flow_ (minimize branching) — fewer decision points for the user
- _analogies & metaphors_ — lean on users' existing mental models
- _transparency & observability_ — users should be able to tell what the system
  is doing
- _group information logically_ — proximity implies relationship
- _balance display density with coherence_ — too sparse wastes attention;
  too dense overwhelms
- _establish & respect standards_ — don't invent novel conventions when
  standards exist
- _minimize task complexity_ — reduce the number of steps to accomplish goals

## the role of alarms

sometimes it's critical to get the user's attention:
- something has gone wrong
- automated system is no longer comfortable proceeding
- time to change course

alarm needs to effectively grab attention:
- flashing lights; annoying sounds; changing colors, shapes
- multiple modalities (don't rely on one channel only)

### failure to alarm effectively

_too many alarms_: information overload / confusion; hard to process → easy
to ignore.

_false alarms_: users react w/ complacency or ignore entirely (the "crying wolf"
effect). reliability of the alarm system in the user's mind degrades.

_intentional disarming_: often a consequence of #1 & #2; users disable
"unnecessary" alarms because responding to them costs valuable time.

result: need _better designed alarm systems_ — appropriate thresholds, triggers,
& sensitivity.

### alarm realities

research shows:
- users often fail to respond _immediately_ — they look for confirmation
- _reliability_ — user's perception of past correlation between alarm & its
  actual value; unreliable alarms get ignored
- users seek _confirmation_: supporting data, second alarm, visual cues
- _expectations & perceptions_ — users become trained to expect alarms under
  certain conditions; novel alarm patterns disrupt this
- _workload & disruptions_ — high workload reduces alarm response effectiveness
- _alarm reduction schemes_ — suppressing nuisance alarms; must be designed
  carefully to avoid suppressing real ones

## building better automation

_**adaptive automation**_ &mdash; periodically pulls the user in; system
decides when to engage the human:
- when user seems disengaged
- during critical events
- when system uncertainty is high

_levels of automation_ — a spectrum from full manual to full auto; the goal
is the most appropriate mix of system & user control for the task.

### design principles for automation

- _only if necessary_ — don't automate for the sake of it
- _routine actions, not high-level tasks_ — automate the predictable low-level;
  leave the novel high-level to humans
- _SA support, not decisions_ — help the user stay aware; don't make the
  decision for them
- _keep user in-the-loop_ — user must always know what the automation is doing
- _minimize modes of automation_ — mode confusion is a major failure mode
- _make state obvious_ — always clear which mode the system is in
- _enforce consistency_ — same behavior across contexts
- _avoid advanced queuing of tasks_ — don't get too far ahead of the user
- _avoid information cueing_ — don't prime the user toward a particular response
- _human/system symbiosis_ — design for collaboration, not replacement
- _provide transparency_ — automation's reasoning should be inspectable

### uninhabited vehicles

a useful extreme case: removing the human from the vehicle entirely.

benefits:
- go where no human can: extreme distance, time, vacuum, pressure
- challenging/dangerous environments: unstable terrain, combat zones
- maintain secrecy & safety: distance from adversary
- full automation possible

challenges:
- somebody still has to drive (remotely): start/stop, left/right, up/down;
  commands transmitted via specified medium w/ latency
- operator without true sensory feedback: sluggish response; delays in
  receiving feedback; missing/misinformation; lack of "big picture"; lack of
  subtle cues (vibration, smell, peripheral vision)
- relatively immature technology
- absence of physical risk can lead to _carelessness_ in the operator
