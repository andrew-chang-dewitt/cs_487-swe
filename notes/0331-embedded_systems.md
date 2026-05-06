---
title: "SWE: Embedded Systems"
description: "Week 11 lecture notes covering embedded sw, real-time systems, systems engineering, systems of systems, timing analysis, & RTOS."
keywords:
  - "embedded systems"
  - "real-time software"
  - "systems engineering"
  - "systems of systems"
  - "RTOS"
  - "timing analysis"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-03-31T11:25-06:00"
---

## agenda

- case study: traffic control system
- embedded systems characteristics & performance
- design considerations
- process coordination & mutual exclusion
- real-time system modelling (state machines)
- real-time design patterns
- timing analysis (deadlines, frequency, execution time)
- systems engineering & sociotechnical context
- systems of systems (SoS)
- real-time OS (RTOS) components
- testing real-time systems

## case study: traffic control system

building on [previous lecture](./0324-ai_assisted_swe.md) on AI-assisted swe
& reuse, we now look at a domain where sw is deeply embedded in physical
infrastructure: traffic control.

a traffic control system is a good motivating example because it hits all the
key characteristics of embedded sw:

- _priorities_: maintain safety & prevent accidents (first); optimize flow of
  vehicles & pedestrians (second)
- _partners_ (the hardware the sw must interact w/):
  - lights & display elements (actuators)
  - sensors: in-road loops, pedestrian buttons, motion sensors, cameras
- _exceptions_: power outages; human error (running lights, jaywalking)
- _assumptions baked into the design_: people know the rules & will follow them;
  people have high situational awareness regarding signaling

> [!TODO]
>
> add traffic control system architecture diagram here — showing sensor inputs,
> control logic, & actuator outputs (lights/displays)

note how much the _assumptions_ matter. a system designed assuming rule-following
users will fail in unexpected ways when users are distracted or impaired.
exception handling must account for violations of design assumptions.

## embedded systems

### characteristics

what makes a system "embedded"?

- _**sw embedded in hw**_ — the sw exists to control or interface w/ specific
  physical hardware; it's not running on a general-purpose computer for a
  general-purpose task
- _**minimal user interface/interaction**_ — often no screen, keyboard, or mouse;
  interaction is with sensors & actuators, not with a human directly
- _**real-time response to environmental change**_ — the system must respond to
  external events within defined time constraints; timing correctness is part
  of functional correctness
- _**product of the environment**_ — behavior is determined by what the sensors
  observe; the system exists to mediate between the physical world & some
  control objective

### performance in embedded context

"performance" means something different here than in a web application:

- _**proper performance**_ = correct response _within an acceptable time_
  — both parts of that are mandatory; a correct answer that arrives too late
  is a wrong answer
- _**availability**_ is expected; you can't tell the traffic light to "try
  again later"
- _**safety & reliability**_ are prominent design drivers — failure modes
  have physical consequences (cars collide, machines injure people, aircraft
  crash)

## design considerations

designing an embedded system involves more dimensions than typical sw:

- _**platform selection**_ — choice of microprocessor/microcontroller; affects
  timing, power consumption, environmental tolerance, available OS support
- _**stimuli response**_ — two types of stimuli:
  - _periodic_ — occur at regular intervals (e.g., check sensor every 100ms)
  - _aperiodic_ — occur at unpredictable times (e.g., pedestrian presses button)
  - design must handle both
- _**timing requirements**_ — hard deadlines vs. soft deadlines; missed hard
  deadline = system failure; missed soft deadline = degraded performance
- _**process architecture**_ — how to aggregate stimuli & response processes;
  which processes run concurrently?
- _**algorithms**_ — computational methods that produce the correct response
  within timing constraints; simpler & faster often wins over elegant
- _**data architecture**_ — shared data structures; synchronization; avoiding
  race conditions
- _**process scheduling**_ — which process runs when; how priorities are managed

## process coordination

real-time embedded systems typically run multiple concurrent processes (or tasks).
coordination is essential:

- processes must share information (sensor readings, state variables, output
  commands) — but uncontrolled sharing causes data corruption
- _**mutual exclusion**_ — when one process is modifying a shared resource, no
  other process should be able to modify it simultaneously; mechanisms: semaphores,
  mutexes, monitors
- _**producer-consumer synchronization**_ — processes may run at different speeds;
  a fast sensor-reading process & a slower processing process need buffering &
  synchronization to avoid data loss or stale reads

failure to handle these correctly produces:

- _race conditions_ — outcome depends on unpredictable timing of events
- _deadlocks_ — two processes each waiting for the other to release a resource
- _priority inversion_ — a high-priority task blocked by a resource held by a
  low-priority task (the Mars Pathfinder bug is the classic example)

## real-time system modelling

the _effect_ of a stimulus may trigger a transition from one state to another.
embedded systems are often best modeled as _state machines_:

- states represent distinct operating modes (e.g., NORMAL, EMERGENCY, FAULT)
- transitions represent responses to stimuli (sensor value crosses threshold,
  timer fires, button pressed)
- outputs (actuator commands) depend on current state & triggering stimulus

_**UML state diagrams**_ are the standard tool for documenting embedded system
behavior — show states & state transitions w/ guard conditions & actions.

> [!TODO]
>
> add example UML state diagram for the traffic control system here — showing
> states: GREEN_NS, YELLOW_NS, RED_NS / GREEN_EW, YELLOW_EW, RED_EW, PEDESTRIAN,
> FAULT; transitions triggered by timers & sensor events

benefits of state-machine modeling:

- makes timing & sequencing requirements _explicit_
- reveals gaps (what happens if stimulus X arrives in state Y?)
- directly implementable as switch-on-state code or with RTOS state machine
  libraries

## real-time design patterns

three common architectural patterns for embedded/real-time systems:

### observe & react

sensors monitored; status displayed or logged; sensor change _initiates_ a
handler. the system watches but doesn't directly control the environment.

example: environmental monitoring system — temperature & humidity sensors
trigger alerts when thresholds are exceeded, but don't directly control anything.

### environmental control

sensors _monitor_ the environment; actuators _adjust_ it. sensor change
initiates signals to actuators that push the environment toward a target state.

example: traffic light controller — sensors detect vehicle presence & pedestrian
requests; actuators (lights) control traffic flow.

### process pipeline

data transformation required before processing; separate concurrent processors
handle transformations in parallel. useful when raw sensor data must be filtered,
compressed, or interpreted before a response can be produced.

example: camera-based traffic monitoring — raw video frames → motion detection
→ vehicle classification → occupancy counting → signal timing adjustment.
each stage is a separate process; pipeline allows stages to run concurrently.

## timing analysis

_correctness of a real-time system depends on both correctness of outputs
**and** time at which they are produced._ timing is not a quality attribute to
optimize — it's a correctness requirement.

timing with mixed periodic & aperiodic stimuli is complex. key factors:

- _**deadlines**_ &mdash; time by which a stimulus must be processed & a response
  produced. _hard deadline_: missing it = system failure. _soft deadline_:
  missing it = degraded service (tolerable sometimes).
- _**frequency**_ &mdash; number of times per second a process must execute.
  a control loop that must respond to a 100 Hz sensor must itself execute at
  ≥ 100 Hz (Nyquist applies here too).
- _**execution time**_ &mdash; time required to process a stimulus & produce
  a response. need _average case_ for planning & _worst case_ for safety analysis.
  worst-case execution time (WCET) analysis is a specialized field.

schedulability: given a set of processes with known frequencies & execution times,
can all deadlines be met? this is a formal analysis problem:

- _**rate-monotonic scheduling (RMS)**_ — static priority assignment; higher
  frequency → higher priority; provably optimal for fixed priorities
- _**earliest deadline first (EDF)**_ — dynamic priority; process w/ nearest
  deadline gets CPU; optimal for dynamic priorities but harder to implement

> [!NOTE]
>
> timing with a mixture of periodic & aperiodic stimuli is difficult to analyze.
> aperiodic events (button presses, faults) can arrive at any time & may require
> preempting periodic tasks. _sporadic server_ algorithms handle this by
> reserving CPU capacity for aperiodic events while preserving schedulability
> guarantees for periodic tasks.

## systems engineering

embedded sw doesn't exist in isolation — it's part of a larger system. systems
engineering considers _all aspects_ of development & evolution of complex systems:

- hardware + sw + processes + people together
- _emergent properties_ — properties of the whole system that don't exist in
  any single component (system safety, system throughput); can't be tested at
  component level alone
- _nondeterminism_ — complex systems may behave differently on each run;
  exhaustive testing becomes impossible
- _reliability of components vs. system_ — a system of highly reliable components
  can still be unreliable if interactions between components create failure modes

### systems engineering process

1. _procurement_ — define overall system requirements
2. _system design_ — architectural design; subsystem identification; integration
   planning
3. _system development_ — build & verify individual subsystems
4. _system integration & testing_ — integrate subsystems; test for emergent
   behavior; verify system-level requirements
5. _deployment_ — install in target environment; operational testing

requirement engineering at the _system_ level is different from sw req engineering:
must capture requirements on hw, sw, processes, & people together. interfaces
between subsystems need explicit specification — often the source of integration
failures.

## systems of systems (SoS)

_**system of systems**_ &mdash; a set of systems that can be used together to
create capabilities not possible w/ any individual system.

examples: air traffic management (radar + communication + scheduling + pilot
decision systems); smart city infrastructure (traffic + utilities + emergency
services).

### types of SoS

- _**directed**_ — centrally managed; constituent systems built specifically to
  work together; clear authority
- _**acknowledged**_ — recognized SoS w/ agreed interfaces but constituent
  systems have independent management
- _**collaborative**_ — constituent systems voluntarily interoperate; no central
  authority; standards-based
- _**virtual**_ — no agreed interfaces & no central management; emergent
  behavior from systems that weren't designed to work together

### SoS challenges

- constituent systems may be _independently owned & managed_ — you can't just
  require them to change their interfaces
- may be _evolutionary_ — new systems join, old systems leave; the SoS must
  handle this gracefully
- _emergent behavior_ is hard to predict — testing at the SoS level is essential
  but difficult
- _autonomy of subsystems_ — each subsystem optimizes for its own goals; may
  conflict w/ system-level goals

## real-time OS (RTOS)

an RTOS provides the runtime environment for embedded real-time sw. components:

- _**real-time clock**_ — drives periodic events; the heartbeat of the system;
  generates interrupts at defined intervals
- _**interrupt handler**_ — manages aperiodic requests; receives hardware
  interrupts from sensors & external events; routes them to appropriate handlers
- _**scheduler**_ — examines process priority & state; decides which process
  runs next; implements RMS, EDF, or other scheduling policy
- _**resource manager**_ — allocates system resources (memory, I/O channels);
  mediates contention between concurrent processes
- _**dispatcher**_ — actually starts execution of selected processes; handles
  context switching (saving & restoring process state)

> [!TODO]
>
> add RTOS architecture diagram here showing relationships between clock,
> interrupt handler, scheduler, resource manager, & dispatcher

common RTOS choices: FreeRTOS (open source, widely used in microcontrollers),
VxWorks (commercial, aerospace/defense), RTEMS (open source, space systems),
QNX (commercial, automotive & medical). choice depends on certification
requirements, hw support, & real-time guarantees needed.

real-time programming languages: C & C++ (dominant; low-level control, no GC
pauses), Ada (strong real-time & safety features; used in defense/aerospace),
Java RTS (real-time garbage collection; used where Java ecosystem matters).

## testing real-time systems

testing real-time sw is harder than testing typical sw:

- _**time-based testing**_ — verify that responses meet their deadlines under
  normal load; requires instrumentation to measure actual response times
- _**load testing**_ — verify timing under maximum expected load; timing that
  works at 50% load may fail at 100%; must test at worst-case arrival rates
- _**fault injection**_ — deliberately inject failures (sensor failures, message
  drops, timing violations) to verify fault handling & recovery; critical for
  safety-critical systems
- _**coverage of timing paths**_ — timing depends on which code path executes;
  WCET analysis requires covering all possible paths

> [!NOTE]
>
> timing defects are often latent — they appear only under specific load patterns
> or hardware conditions. this makes them especially dangerous in safety-critical
> embedded systems. continuous monitoring of timing metrics in production (where
> feasible) provides the most realistic data on timing behavior.

the combination of concurrent processes, real-time constraints, & close hw
integration makes embedded systems some of the most challenging sw to develop
& test correctly. the discipline required is high — & the stakes often are too.
