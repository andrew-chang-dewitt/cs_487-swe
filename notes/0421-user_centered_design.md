---
title: "SWE: User-Centered Design"
description: "Week 14 (final) lecture notes covering UCD process, usability goals, evaluation approaches, SA-focused design principles, & keeping it simple."
keywords:
  - "user-centered design"
  - "UCD"
  - "HCI"
  - "usability"
  - "situational awareness"
  - "evaluation"
  - "design principles"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-04-21T11:25-06:00"
---

## agenda

- HCI & UCD defined
- give the people what they want?
- the UCD design process
- responsibilities of the designer
- usability goals
- design principles
- evaluation described & approaches
- evaluation methods & usability testing
- measuring usability
- UCD & situational awareness
- SA-focused design principles
- keep it simple

## HCI & UCD

this is the final lecture of the semester. building on last week's
[previous lecture](./0414-human_awareness_design.md) on situational awareness &
human awareness design, we now look at the _process_ side of designing for humans:
user-centered design.

_**human-computer interface (HCI)**_ &mdash; the means of interaction between
human users & a computer system. if we automate a human's role, the HCI becomes
a computer-computer interface — the design challenge shifts but doesn't disappear.

_**user-centered design (UCD)**_ &mdash; a design methodology that:
- _involves the user_ in the design process throughout
- _emphasizes user performance_ in the evaluation of design (not designer
  preference, not feature count)

## give the people what they want?

key mindset shifts for UCD:

- _the user's opinion is more important than yours_ — the designer's aesthetic
  preferences & assumptions don't override actual user behavior
- _appreciate users' capabilities_ — don't underestimate or overestimate; meet
  them where they are
- _offer help — in many forms_ — different users need different kinds of help
- _strive for quality user experiences_ — "good enough" is not good enough
- _involve the user early_ — don't design in isolation & then hand it to users
  for the first time at launch
- _use what works_ — draw on established patterns & standards; don't reinvent
  unnecessarily
- _things can be interpreted differently by different people at different times_
  — design for interpretation variability, not just the happy path

> [!NOTE]
>
> this is a harder mindset to maintain than it sounds. designers (including sw
> engineers) tend to build for themselves. UCD is a discipline of deliberately
> resisting that tendency.

## the UCD design process

1. _identify user groups_ — who will actually use this? multiple groups may
   have different needs, capabilities, & goals
2. _establish requirements for the user experience_ — what does success look
   like for each user group?
3. _develop alternative designs_ — don't commit to the first idea; explore the
   design space
4. _create interactive prototypes_ — low-fidelity → high-fidelity; get
   something in users' hands early
5. _evaluate with relevant, objective analysis_ — measure against requirements;
   use appropriate evaluation methods (see below)
6. _collect feedback & fix it in the next version_ — UCD is iterative; design
   never fully "finishes"

> [!TODO]
>
> add UCD process loop diagram here — showing the iterative cycle: identify →
> requirements → design → prototype → evaluate → feedback → back to design

## responsibilities of the designer

- users should _enjoy_ the experience (or at minimum not be frustrated)
- product should undeniably _ease or improve_ the user's life:
  - increased productivity
  - reduced anxiety / minimal frustration
  - better performance & results
  - consistency, integrity, reliability
- product should _exceed competing products_ in these areas:
  - customers will pay more for better UX
  - customers will buy variant products from the same maker
  - customers will tell their friends (or the internet)

the last bullet is the business case for UCD: good UX is a competitive advantage.

## usability goals

_**usability**_ &mdash; the extent to which a product can be used by specified
users to achieve specified goals with effectiveness, efficiency, & satisfaction.

the standard set of usability goals:

- _effective to use_ — users can accomplish their goals at all; errors don't
  prevent task completion
- _efficient to use_ — tasks can be accomplished with minimal steps & time
- _safe to use_ — prevents errors; recovers gracefully when errors occur;
  doesn't put users in danger
- _having good utility_ — provides the right functions for the right tasks
- _easy to learn_ — time-to-competence is low; new users can get started quickly
- _easy to remember how to use_ — returning users can re-engage without
  relearning from scratch (learnability vs. retainability are distinct goals)

## design principles

- _make it visible, or not, as needed_ — important things should be perceptible;
  implementation details should be hidden
- _provide feedback_ — every action should produce a perceptible response;
  users should always know what the system is doing
- _set boundaries (constraints)_ — prevent invalid actions; make it hard to
  do the wrong thing
- _be consistent_ — same action, same result, everywhere; violating consistency
  breaks users' mental models
- _provide clues_ — affordances (handles look graspable; buttons look pressable);
  labels; icons; progressive disclosure

## evaluation described

_**evaluation**_ &mdash; process of assessing goodness / acceptability of a
design against specified criteria.

_why_: critical to achieving user acceptance; far cheaper to fix problems early
(prototype stage) than after deployment.

_what_: criteria should match users' needs & interests — easy to learn, fast,
satisfying, entertaining (depending on the product).

_where_: lab (control) vs. field (user's natural setting — less control, more
ecological validity). tradeoffs exist; neither is always superior.

_when_: can evaluate at any point in the design process; the question is
whether the artifact is mature enough to yield useful data & actionable
feedback.

### evaluation approaches

_**usability testing**_ &mdash; quantification of user performance:
- time to complete tasks
- error rates; type & severity of errors
- measures typical users on typical tasks
- controlled by evaluator; conducted in lab or controlled setting

_**field studies**_ &mdash; observe users in their natural setting:
- higher ecological validity
- less control; harder to measure precisely
- reveals real usage patterns that lab studies miss

_**analytical evaluation**_ &mdash; no users directly involved:
- _heuristic evaluation_: expert evaluators apply guidelines & standards
  to identify usability problems (Nielsen's 10 heuristics are the canonical
  example)
- _cognitive walkthrough_: step through tasks as a user would; identify
  where understanding breaks down

_**hybrids**_ — mix & match as the situation demands.

## evaluation methods

_**observation & inquisition**_:
- observe users (think-aloud protocol)
- ask users (questionnaires, interviews)
- ask experts (heuristic evaluation, expert review)

_**user testing**_: based on defined scenarios; representative users perform
tasks; performance is measured.

_**inspections**_: based on heuristics; no users; evaluators assess compliance
with known usability principles.

_**modeling**_: cognitive models (GOMS, Fitts's law) used to predict performance
& establish benchmarks before any user testing is done.

### usability testing detail

_**usability test**_ &mdash; testing the product to determine the extent to which
it is usable by the intended user population on the tasks for which it was designed.

methods:
- _logging_ — keystrokes, mouse movements, eye tracking; reveals what users
  actually do (not what they say they do)
- _video recording_ — capture facial expressions, body language, hesitations
- _think-aloud protocol_ — users narrate their thought process; reveals
  mental models & confusion points
- _user satisfaction questionnaires/interviews_ — how do you feel?
  efficiency & effectiveness from the user's perspective

## measuring usability

time-based metrics:
- _time to complete_ a defined task
- _time to re-learn_ after a specified period away from the product

count-based metrics:
- _errors made_ per task
- _errors per unit time_
- _navigations to help_ — proxy for confusion
- _number of users making a particular error_ — reveals systematic problems
- _number of users completing successfully_ — the most fundamental measure

> [!TODO]
>
> add example usability test scorecard here — showing tasks on rows, metrics
> (time, errors, success) on columns

## UCD & situational awareness

connecting back to last week's SA material: UCD is the _process mechanism_
by which we achieve good SA support.

traditional decision-support design is _technology-centered_: start with the
sensors, reports, gauges, & alarms available, then build a UI around them.
result: information overload, bottlenecks, 7 ± 2 chunk limits exceeded,
high recall & processing time demands.

stat worth knowing: operator error is a causal factor in 60–85% of all
accidents. UCD, by improving the human side of the human-machine system, is
directly addressing the largest single source of failures.

UCD is _not_:
- giving users everything they ask for (≠ user-led design)
- making decisions for them (≠ automation-first)
- doing things for them (≠ removing human agency)

UCD _is_:
- organizing technology around users' needs & capabilities
- organizing around the way users process information & make decisions
- keeping the user in control & aware of state — thereby reducing anxiety
  & improving decision-making effectiveness

### SA-focused design principles

at the intersection of UCD & SA theory:

- _provide support for projection_ — give users what they need to anticipate
  future states (level 3 SA); trend lines, forecasts, early indicators
- _provide support for confirmation_ — let users verify their understanding
  against reality; don't make them guess
- _remove ambiguity_ — ambiguous displays force users to interpret; interpretation
  takes time & introduces error
- _reduce false alarms_ — every false alarm trains users to ignore alarms;
  calibrate thresholds carefully
- _set trade-offs appropriately_ — when displaying partial information is
  necessary, make the trade-off explicit
- _use multiple modalities, consistently_ — visual + auditory + haptic; but
  consistency across contexts is required or users get confused
- _minimize disruptions_ — every disruption costs SA recovery time
- _support assessment & diagnosis of multiple alarms_ — when many alarms fire
  simultaneously, users need help distinguishing root cause from symptoms
- _support global SA_ — don't optimize only for local/detail view; maintain
  access to the big picture

## keep it simple

working memory is limited — 7 ± 2 chunks. designing with this limitation
in mind is _critical_, not optional.

_less is more_:
- avoid clutter — every element costs attention
- avoid unnecessary marks & decorative elements — every pixel requires a reason
- avoid scrolling & paging — if users must page to find information, the
  information architecture is failing
- slick, cool, & flashy are not design goals — they are often inversely
  correlated w/ usability

_organization is key_:
- group logically & summarize where possible — chunking reduces working memory
  load
- focus on context — surface the information relevant to the current task;
  hide the rest
- rely on iconic memory where possible — visual patterns processed pre-attentively
  don't consume working memory; use color, shape, & position consistently to
  encode meaning

> [!NOTE]
>
> this is where UCD, SA, & complexity design principles all converge. the
> common thread: _design for human cognitive limits, not for feature completeness._
> an interface that displays everything is an interface that communicates nothing.

---

_that's it for the semester. the arc from sw processes → requirements → design
→ testing → resilience → AI → embedded systems → SOA → human awareness → UCD
traces a complete picture of what swe actually is: not just writing code, but
systematically managing complexity, risk, & human factors to build systems that
work in the real world._
