---
title: "SWE: Software processes & agile development"
description: "Week 2 lecture notes, introducing concepts of software engineering processes & the agile method."
keywords:
  - "agile"
  - "software engineering methods"
  - "lecture notes"
  - "computer science"
  - "cs 487"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-01-20T11:25-06:00"
  updated: "2026-01-22T11:25-06:00"
---

## agenda

- sw proc models
  - waterfall
  - incremental development
  - reuse-oriented sw engineering
- what else is there?
  - iterative approach
  - ex: spiral model
  - ex: rational unified process
- agile approaches

## sw proc models

in the [last lecture](./0115-motivations.md) we discussed why this
matters & touched on defects in software products. software process
models aim to address the problem of defects by applying prescribed
approaches to the development process with the goal of increasing
likelihood that end product meets goals & has less defects than it
would w/out.
some generic models you may have heard of include:

- waterfall
- incremental development
- reuse-oriented sw engineering

each of these models addresses the key needs, attempting to ensure a
quality product is produced.

- specification of requirements
- design & implementation
- verification & validation
- evolution

all sw proc models have some notion of separating the process into
phases, including some of the following:

- initiate/contract/feasibility
- analyze/requirements engineering
- design/architect
- build/implement/code
- test/verify/validate/assess/review
- release
- maintain

these phases are seen throughout a the following common generic models
for sw development:

### generic method #1: waterfall

roughly composed of the phases:

1. analyze
2. design
3. build
4. test

has the unique characterstic of viewing sw dev as water, incapable of
going uphill. positions each phase above the following phases & then
models effort/progress as water flowing through the phase to the "gate"
at the end. once project owners/stakeholders/whoever sign off on the
phases' output, the gate opens & effort moves downhill to the next
phase.

this structure is rigidly enforced & prohibits moving backwards or
forwards from the current phase. it is forbidden to go back to a
previous phase, even if a problem w/ the output of said prev. phase is
previous phase, even if a problem w/ the output of said prev. phase is found.

intends to increase likihood that project actually ever reaches a
"done" point. however, it comes w/ problems:

- difficult to estimate completion time because any one phase can hold
  up the entire process indefinitely
- in practice, forbids iteration, making it difficult to really learn
  from each phase/previous phases

basing this model on the idea of "gravity" pushing the process
"downhill" (forward in time) ignores the fact that time already moves

### generic method #2: incremental development

takes a more realistic approach & remembers that the process is always
moving forward w/out need for "gravity". in doing so, it allows for

works by splitting end product goal into individual, functional
"sub-objectives" that together comprise a functional product. each
iteration of the process aims to achieve a single sub-objective before
starting the next iteration. by focusing on answer questions &
resolving challenges in an iterative fashion, this method delivers
portions of the final product in an incremental fashion, allowing for
learning as progress is made.

benefits:

- produces a prototype early
- can begin getting feedback early
- allows for faster learning

### generic method #3: reuse-oriented sw engineering

attempts to speed up the process by focusing on (re)using things
already created/existing at the cost of possibly not perfectly matching
requirements. can increase complexity & requires strong discipline
(documentation, testing, version control, modular design) in managing
reusable portions of products.

## what else is there?

the three generic models discussed above all have to contend with the same problem: change happens.

as such, engineering organizations have gravitated towards iterative
approaches. this allows them to rapidly evolve w/ technology, respond
to competition more quickly, & adjust in the face of changing economic
conditions. to enable iterative approaches to have better success, it
has been found that shorter, well-defined iterations are helpful at
lowering risk of change before some milestone. additionally, this
allows customers to use the product faster, receiving incremental
upgrades/new features/etc.

most imporantly, iterative approaches allow for integrating process improvement tightly with the development process of a project. if viewed as an iterative cycle of try-learn, a process inherently embraces that failure is likely by allowing for failure so that it can be learned from before trying again. two common process improvement outcomes that get focused:

- process maturity (CMM)
- reuducing overhead (Agile)

### iterative ex #1: spiral model

developed by Barry Boehm, each iteration executes 4 phases repeatedly while growing a product w/ each completion of an iteration:

1. objective setting
2. risk assessment & reduction
3. development & validation
4. planning for next iteration

> [!TODO]
>
> study & redraw diagram from slides below

```no-linenums

```

### iterative ex #2: rational unified process

Based on UML & the Unified Software Development Process, this is a hybrid model that incorporates prototyping & incremental delivery of product releases. Describes the process from multiple perspectives:

- dynamic: phases of the model over time
- static: process activities that are enacted
- practice: suggests good practices to use during the process

also executes 4 phases repeatedly:

1. inception
2. elaboration
3. construction
4. transition

## agile approaches

a dominant model of the software development process, the agile method
attempts to speed up delivery when aiming at a moving target while
heavily involving users as early as possible & focus on extreme
flexibility.

some characteristics of agile processes:

- interwoven phases (overlap between them instead of hard boundaries)
- documentation effort is minimized
- frequent delivery of product releases
- visual development tools to facilitate rapid UI dev

typically looks roughly like the following, prioritizing "flow" to keep
forward momentum high. starts by getting a basic idea of the goal & how
to get there, then jumps right into iterations of:

1. design small portion
2. implement it
3. deliver it, surfacing evolutions at frequent intervals
4. repeat

> [!WARNING]
>
> it's not always appropriate to use an agile approach!
>
> sometimes, stability of process is a key requirement, especially for
> large-scale efforts across the entirety of a large organization or
> for critical systems that require absolute success of some key
> feature/requrement/etc.

agile shines in small efforts/teams, less-than-critical systems & can
easily be integrated as part of a larger effort towards some major
milestone.

### extreme programming (XP)

a subset of the agile method, this approach pushes things to the extreme:

- vvv small teams
- vvv rapid dev & release cycles
- vvv close user involvement

characterized by:

- requirements given as simple "user stories"
- change handled by frequent code/test/release iterations
- chasing simplicity to sustain the rapid pace

products created through the XP process can often be difficult to test using conventional, independent testing team due to a lack of formal system specification. instead, testing is usually done by the developers, often by approaches like test-driven development (TDD). this is enforced by only accepting code considered "clean" into the current version (mainline branch) using rules like:

- create tests first, then write code to pass them
- use tests as a product specification
- get users involved in writing tests! (e.g. have users show how they
  would use the product in a low-fi prototype, then write tests to
  replicate that)
- use automation as much as possible
