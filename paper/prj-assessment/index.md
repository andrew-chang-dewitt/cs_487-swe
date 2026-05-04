---
meta:
  skipRenderTitle: true
---

:::hgroup{#titlepage.titlegroup}

# Team E: Individual Assessment

Andrew Chang-DeWitt \
CS 487 - Software Engineering \
Illinois Institute of Technology \
Spring 2026

:::

## 1. Team experience & my role

My role across the 5 project phases:

1. Analysis report
   - Functional requirement design (user stories)
2. Test plan
   - Defined inputs & expected outputs for functional requirements test cases
3. Design report
   - Data perspective & risk assessment
4. Design review
   - Updates amendments since previous submission
5. Final report & presentation
   - Collaborated on final presentation as well as section 2 & 4 of the final report
   - Backend product development
     - wrote FastAPI server code & unit testing
     - wrote database schema & automated database management as part of build system
   - Protopye code quality
     - performed code reviews
     - automated quality requirements as part of CI/CD workflow

## 2. Teammate roles & team performance

### 2.1 Teammate roles

:::{.outline}

1. Peter Capuzzi
   1. Analysis report
      - User category analysis
   2. Test plan
      - User persona design
   3. Design report
      - UI models & flow navigation
   4. Design review
      - Planned use of AI
   5. Final report & presentation
   - Frontend product development (wrote the entire frontend application)
   - Wrote section 1 & collaborated on section 2 of the final report document
   - Collaborated on Final presenatation document & recorded product demo video
2. Derrick Taylor
   1. Analysis report
      - Non-functional requirement analysis
   2. Test plan
      - Non-functional test case design
   3. Design report
      - Algorithmic perspective & exception management
   4. Design review
      - Prototype completeness description
   5. Final report & presentation
      - Collaborated on final presentation
3. Rinat Verezub
   1. Analysis report
      - Intro, contributed to User category analysis, & conclusion
   2. Test plan
      - Summary sections & user persona design
   3. Design report
      - Overview, system/context model, non-functional design, & AI use
   4. Design review
      - Assessment of proposed design
   5. Final report & presentation
      - Wrote devops processes & code (docker containerization & inter-layer communications)
      - Created final presentation template
      - Performed code reviews of prototype code
   6. Overall contributions: Accross all areas of the project, Rinat was the defacto team leader & organizer. If it weren't for the proactive steps Rinat took for each deliverable to get us started & begin defining what work needed to be done, all of our jobs would have been much harder.

:::

### 2.2 Team performance

Overall, the team worked quite well together. The process of delivering each phase was highly organized & communication was typically well managed & timely. Near the end of the project there was some difficulty getting what felt like equitable contributions from all team members (Peter & I wrote nearly the entire application ourselves, while Rinat orchestrated the rest of the deliverables; however, Derrick was difficult to reach during the entire period we were working on final deliverables).

## 3. Automation of my role

Some aspects of my role are not very open for more automation:

- system design review
- code review&mdash;while AI is great at catching weird edge cases across distant parts of an application, it is _not_ great at understanding whole systems or end users. additionally, it is a bad judge of actual code quality, often overlooking basic things.

Some aspects that could have been more automated:

- code generation&mdash;particularly in the areas of
  - test data generation, & repetition of test case implementations
    - by using AI to handle more test case generation & more of the tedious repetition
    - by using parameterized test methods to make testing more DRY
  - database query logic
    - by using AI to infer data shape from database schema & api endpoint inputs/outputs
  - implementing additional endpoints for other features that we did not get time to develop

## 4. Assesment of AI tool use throughout project

Tools used:

- GitHub Copilot
  - most helpful for code review (a fast, on-demand second opinion with a great memory for documentation & distantly related portions of the code base)
- Microsoft Copilot
  - During test planning for assistance in writing test cases from feature user stories
  - Useful for finding inconsistencies in writing & for reviewing writing

Overall, this project & course was instrumental in getting me to actually give AI usage a chance. By encouraging its use in some areas, I found myself moving past my more Luddite-adjacent stances regarding AI at a time when adoption of its use where it _can_ be helpful is critical to obtaining employment.

## 5. Future application of lessons learned

### 5.1 Early, effective devops

Good devops matters & it matters earlier than I thought. It would have saved us a lot of headaches to have implemented full end-to-end communication for at least one minor feature (even just a simple status/hearbeat check) that touched all three layers of the system (frontend, backend, database) to be sure they could be easily developed together & deployed.

### 5.2 Good management

Having a well-organized & proactive manager to get the team going early & keep them moving when things appear to be stagnating is perhaps the most important thing to success. Without the contributions in this area made by Rinat, I don't how we would have gotten everything done.
