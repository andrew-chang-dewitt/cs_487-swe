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
---

## agenda

- sw proc models
  - life-cycle phases
  - waterfall
  - incremental development
  - reuse-oriented sw engineering
- dev proc activities
- what else is there?
  - iterative approach
  - ex: spiral model
  - ex: rational unified process
- how can we do better?

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

### life-cycle phases

most sw proc models have some notion of separating the process into phases, including some of the following:

- initiate/contract/feasibility
- analyze/requirements engineering
- design/architect
- build/implement/code
- test/verify/validate/assess/review
- release
- maintain

these phases are seen throughout a the following common generic models for sw development:

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

takes a more realistic approach & remembers
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
