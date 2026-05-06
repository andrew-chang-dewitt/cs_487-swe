---
title: "SWE: Artificially Intelligent Systems"
description: "Week 7 lecture notes covering AI in sw engineering, safety-critical systems, hazard analysis, security engineering, & designing for dependability."
keywords:
  - "artificial intelligence"
  - "safety engineering"
  - "security engineering"
  - "hazard analysis"
  - "safety-critical systems"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-02-24T11:25-06:00"
---

## agenda

- human awareness & exception detection
- automated exception management
- AI: opportunities & risks
- safety-critical systems defined
- hazard-driven analysis
- requirements driving design
- safety engineering processes
- designing for security (revisited w/ AI lens)
- common vulnerabilities
- security testing

## human awareness & the automation paradox

building on [previous lecture](./0217-risk_managementand_exception_handling.md)
on risk & exception management, this week we bring AI into the picture — what
happens when machines take over tasks that humans used to perform?

### human exception detection

humans detect exceptional states in a process that looks a lot like the computer
system exception detection we discussed last week:

- assume a normal operating state
- sense deviations from that normal state
- recognize the current state _as_ exceptional

but there's a critical human-specific failure mode: _disengagement_. one of the
fundamental benefits of automation is that it frees humans from the need to
continuously monitor & intervene. but that disengagement is also a problem —
if a human is too disengaged from an automated system, they won't "receive the
message" when an exception occurs. they've mentally checked out.

> [!NOTE]
>
> this is sometimes called the "out-of-the-loop" problem in human factors
> research. automation that works too well can degrade operator skills & awareness
> over time, making them _less_ capable of handling edge cases when automation
> fails.

### human exception handling

once a human _does_ recognize an exceptional state, the handling protocol matters:

- protocol should specify a clear set of actions to return to at least a "safe"
  state if not the fully normal state
- _acknowledgement-based verification_ is critical — the system must confirm
  that the human has received the alert, responded, & taken control; you can't
  just fire a notification & assume it was seen

## automated exception management

when we hand exception management to automated systems, the same two-step
structure applies: _detection_ then _handling_.

### automated detection

- _first step_: recognizing the problem exists at all
- characteristics of the exceptional state must _clearly distinguish_ it from
  every other possible state
- failure modes:
  - system doesn't recognize the characteristics as exceptional → no response
  - system _mis-identifies_ them as a _different_ kind of exception → wrong
    handler fires
- the harder you've worked to enumerate possible exceptional states, the more
  robust detection becomes — but you can never enumerate all possible states

### automated handling

once the exceptional state is detected:

- system must _quickly_ execute handling code to recover (lag time is the enemy)
- ideal recovery: return to the fully normal operating state
- acceptable recovery: transition to an agreed-upon "safe" state
- critical failure: no handler exists for this exceptional state → what happens?
  - system crashes? silently continues? enters undefined behavior?
  - this is the design gap that causes the most harm in safety-critical AI systems

## AI: opportunities & risks

### opportunities

AI & automation bring genuine capabilities:

- _**consistency**_ &mdash; machines don't get tired, distracted, or emotional
- _**correctness**_ (within training distribution) &mdash; can outperform humans
  on well-defined tasks w/ clear rules
- _**speed**_ &mdash; can process & react far faster than humans
- _**cost effectiveness**_ &mdash; scales without proportional increase in labor
- _**mission-critical operation**_ &mdash; can operate in environments too
  dangerous for humans

### risks

the risks are significant & under-appreciated:

- _**bias**_ &mdash; learned from historical data that may encode past
  discrimination or skewed sampling; outputs reflect & amplify those biases
- _**lack of transparency**_ &mdash; modern ML models (especially deep neural
  nets) are often "black boxes"; we can observe inputs & outputs but not
  the reasoning; makes auditing & debugging extremely hard
- _**drift**_ &mdash; the world changes; a model trained on old data may become
  progressively less accurate over time as the distribution of inputs shifts
- _**hallucinations**_ &mdash; generative AI models can produce confident,
  fluent, but entirely fabricated outputs; there's no internal truth-check
- _**loss of control of mission-critical systems**_ &mdash; especially
  dangerous when AI encounters unexpected exceptions it wasn't trained on; the
  automated handler doesn't exist for this case
- _**loss of human understanding / institutional knowledge**_ &mdash; when
  processes are fully automated, humans may lose the understanding needed to
  override or repair the system when it fails

> [!WARNING]
>
> the interaction between _AI risks_ & _safety-critical systems_ is the core
> concern of this lecture. AI introduces a new class of exception: the exception
> the system was never trained to recognize. unlike traditional sw where you
> can enumerate expected & unexpected states, AI systems can fail in ways that
> are fundamentally unpredictable from the training data alone.

## safety-critical systems

_**safety-critical system**_ &mdash; a system whose operation must _always_
be in a safe state; failure must not harm people or the environment.

two categories (same as last week, but worth revisiting w/ the AI lens):

- _**primary safety-critical**_ &mdash; embedded controllers where sw failure
  directly causes hw malfunction resulting in injury or environmental damage
  (aircraft autopilots, autonomous vehicles, medical devices)
- _**secondary safety-critical**_ &mdash; sw that doesn't directly control
  safety hw, but whose failure could cause harm indirectly (a defective AI
  tool that designs flawed systems)

the non-functional requirement for safety-critical systems: _system operation
must always be in a safe state_. this is an absolute constraint — not a target
to be balanced against cost or performance.

## hazard-driven analysis

the standard engineering approach to safety-critical sw development:

### hazard identification

imagine the hazards that may threaten the system. this is partly analytical
(systematic enumeration of failure modes) & partly creative (imagining novel
failure scenarios). the slides' use of "imagine" matters — you have to
_think ahead_ to failure states that haven't happened yet.

### hazard assessment

prioritize identified hazards:

- _likelihood_ &mdash; how probable is this hazard?
- _severity_ &mdash; how bad would it be if it occurred?
- _detectability_ &mdash; would we know it had occurred?

low-priority hazards (low likelihood × low severity) may not justify further
engineering effort. high-priority hazards drive the design.

### hazard analysis

root-cause analysis: map the early events that lead to each high-priority
failure. tools include:

- _fault tree analysis_ &mdash; top-down decomposition of failure events into
  contributing causes
- _FMEA (Failure Mode & Effect Analysis)_ &mdash; bottom-up: for each component,
  what are the failure modes & what are their effects?

### risk reduction

identify factors that reduce likelihood and/or impact:

- design out the hazard (eliminate the root cause)
- detect & remove the hazard before it causes harm
- limit damage when hazard occurs (containment)

## requirements drive the design

much of design is choosing the best solution by evaluating how well it satisfies
prioritized NFRs. for safety-critical systems, the evaluation criteria are:

- _**hazard avoidance**_ &mdash; system designed to avoid situations where
  hazards can occur; don't go near the dangerous state
- _**hazard detection & removal**_ &mdash; system detects problems & corrects
  them _before_ an accident occurs; sensors + automated response
- _**damage limitation**_ &mdash; when problems do occur, minimize their impact;
  design for graceful degradation

these three strategies should all be applied in layers. relying on any one
alone is insufficient.

> [!TODO]
>
> add design evaluation matrix from slides showing NFRs × design options here

## safety engineering processes

### safety assurance

defining & executing activities which provide evidence of safe operation:

- safety planning (what will we do to assure safety?)
- safety case development (structured argument that the system is safe)
- independent safety auditing
- safety reviews at each development milestone

### formal verification

applying _formal methods_ — mathematical proof of correctness — to safety-critical
components. tools include:

- _Z notation_ &mdash; set-theory-based formal spec language
- _TLA+_ &mdash; temporal logic of actions; good for concurrent systems
- _model checking_ &mdash; exhaustive exploration of state space using tools
  like SPIN or NuSMV

formal verification gives high confidence but is expensive & doesn't scale well
to large systems. typically applied to the most critical components only.

### model checking

modeling the system's state behavior & using (often automated tool-based)
assessment to check properties of that model. can exhaustively prove that certain
bad states are unreachable — within the model. the caveat: the model may not
perfectly represent the implementation.

### static program analysis

tool-based assessment of source code to discover possible faults & anomalies
without executing the code. examples:

- type checkers
- data-flow analysis (use before define, unreachable code)
- concurrency analysis (potential deadlocks, race conditions)
- bounds checking

combines well w/ code inspections. static analysis is particularly valuable
for safety-critical code because it can catch entire classes of defects
mechanically.

> [!TODO]
>
> add diagram of safety engineering V-model from slides/book here

## designing for security (w/ AI context)

the security design principles from last week apply here, but they take on added
importance when AI systems are involved (since AI systems have a larger &
less predictable attack surface):

- _**explicit security policy**_ &mdash; base decisions on clearly documented
  policies; don't rely on implicit assumptions; especially important for AI
  systems where behavior may not be fully predictable
- _**defense in depth**_ &mdash; multiple layers of security; no single control
  is assumed to be sufficient; if the AI layer is compromised, other controls
  still apply
- _**fail securely**_ &mdash; when the system fails (& it will), it should
  fail into a safe & secure state, not an open one; for AI: if the model
  returns low-confidence output, fall back to a safe default rather than
  acting on uncertain output
- _**balance security & usability**_ &mdash; security controls that interfere
  with usability get bypassed; PINs are a classic example of "good enough"
  security that users will actually use
- _**log user actions**_ &mdash; audit trail for forensics & accountability;
  critical for AI systems where the reasoning is opaque — at least you can
  see what the system did even if not why
- _**redundancy & diversity**_ &mdash; maintain backups; avoid reliance on a
  single potentially vulnerable platform; for AI: diverse model implementations
  reduce risk of correlated failures
- _**specify & restrict input formats**_ &mdash; validate & sanitize all inputs;
  for AI systems: prompt injection & adversarial inputs are real threats;
  input validation is the first line of defense
- _**compartmentalize assets**_ &mdash; user "need to know" principle; AI
  systems should only have access to the data & systems they actually need
- _**design for deployment**_ &mdash; proper & secure default configuration;
  don't ship with unnecessary permissions or debug endpoints enabled

### common vulnerabilities (from ch. 13)

- _**injection attacks**_ (SQL injection, prompt injection for LLMs) &mdash;
  attacker inserts malicious input that is interpreted as code or commands
- _**buffer overflows**_ &mdash; write past the end of a buffer; corrupt
  adjacent memory; classic in C/C++; less relevant in managed languages
- _**cross-site scripting (XSS)**_ &mdash; attacker injects scripts into web
  pages served to other users
- _**cross-site request forgery (CSRF)**_ &mdash; attacker tricks authenticated
  user's browser into making unintended requests
- _**privilege escalation**_ &mdash; user gains more permissions than authorized

for AI-specific systems, add:

- _**adversarial inputs**_ &mdash; carefully crafted inputs that cause the model
  to produce incorrect outputs (e.g., images w/ imperceptible perturbations that
  fool classifiers)
- _**data poisoning**_ &mdash; attacker corrupts training data to embed
  vulnerabilities or biases into the deployed model
- _**model extraction**_ &mdash; repeated queries allow attacker to infer &
  reproduce a proprietary model

### security testing

- _**penetration testing**_ &mdash; authorized attack simulation; try to break
  in using the same techniques an attacker would
- _**vulnerability scanning**_ &mdash; automated tools scan for known
  vulnerability patterns
- _**code review**_ &mdash; manual inspection specifically looking for security
  defects; particularly important for input handling & authentication logic
- _**red team / blue team**_ &mdash; red team attacks, blue team defends;
  adversarial simulation of real attack scenarios

> [!NOTE]
>
> security is not just technical — it also involves people, processes, &
> organizational policies. the strongest technical controls can be defeated
> by social engineering (phishing, pretexting). a complete security strategy
> addresses all three: technology, process, & people.

## the bigger picture: AI & sw engineering

AI creates a new engineering challenge that traditional sw engineering processes
weren't designed for: _the behavior of the system is not fully specifiable in
advance_. traditional sw: you write the logic, you can read it, you can prove
properties about it. ML-based AI: the "logic" is encoded in billions of
parameters learned from data; you can't read it; proving properties is hard.

this means:

- _hazard analysis_ becomes more complex: you have to imagine failure modes that
  emerge from unexpected combinations of training data & inputs
- _formal verification_ is largely inapplicable to the learned components
  (though it can still be applied to safety envelopes around them)
- _testing_ becomes more important but also harder: how do you test for correct
  behavior across an effectively infinite input space?
- _monitoring & runtime safety_ become critical: since you can't fully verify
  behavior in advance, you need to watch what the system actually does in
  production & have mechanisms to intervene

the engineering discipline of _safety-critical AI_ is still evolving. the
frameworks from ch. 12 & 13 (hazard analysis, defense in depth, formal
methods where applicable, rigorous testing) give us the best starting point
we have — applied with extra care & humility about what we don't know.
