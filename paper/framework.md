# Engineering Awareness to Achieve Safe AI

Andrew Chang-DeWitt \
CS 487 - Software Engineering \
Illinois Institute of Technology \
Spring 2026

::ref-reset

::ref-item{type="arxiv" id="amodei" leadLastName="amodei" authors="Dario Amodei, Chris Olah, Jacob Steinhardt, Paul Christiano, John Schulman, Dan Mané" year="2016" title="Concrete problems in AI safety" arxivId="1606.06565" link="https://arxiv.org/abs/1606.06565"}

::ref-item{type="online-doc" id="nist" authors="National Institute of Standards and Technology (NIST)" year="2023" title="AI risk management framework (AI RMF 1.0)" website="U.S. Deptartment of Commerce" retreived="March 11, 2026" link="https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf" archive="https://web.archive.org/web/20260309212727/https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf"}

::ref-item{type="online-doc" id="gubkin" authors="Alon Gubkin" month="June" year="2025" title="Comprehensive evaluation metrics for ai observability" website="Coralogix" retreived="March 11, 2026" link="https://coralogix.com/ai-blog/evaluation-metrics-for-ai-observability/"}

::ref-item{type="journal" id="rahwan" authors="Iyad Rahwan, Manuel Cebrian, Nick Obradovich, et al" year="2019" title="Machine behaviour" journal="Nature" volNum="568" month="April" pageNum="477-486" link="https://doi.org/10.1038/s41586-019-1138-y"}

::ref-item{type="arxiv" id="barenji" authors="Reza Vatankhah Barenji, Sina Khoshgoftar" year="2025" title="Agentic AI for autonomous anomaly management in complex systems" link="https://doi.org/10.48550/arXiv.2507.15676" arxivId ="2507.15676"}

::ref-item{type="journal" id="langer" authors="Markus Langer, Kevin Baum, Nadine Schlicker" month="Nov." year="2025" title="Effective Human Oversight of AI‑Based Systems" link="https://doi.org/10.1007/s11023-024-09701-0" journal="Minds and Machines" volNum="35" articleNum="1"}

::ref-item{type="journal" id="hwang" authors="Jin young Hwang" month="Sept." year="2024" title="Ethics of artificial intelligence: examining moral accountability in autonomous decision‑making systems" link="https://doi.org/10.30574/wjarr.2024.23.3.2884" journal="World Journal of Advanced Research and Reviews" volNum="23" issueNum="3" pageNum="3192-3198"}

::ref-item{type="proceedings" id="phan" authors="Dung T. Phan, Radu Grosu, Nils Jansen, Nicola Paoletti, Scott A. Smolka, Scott D. Stoller" day="11-15" month="May" year="2020" title="Neural simplex architecture" conference="NASA Formal Methods: 12th International Symposium (NFM 2020)" location="Moffett Field, CA, USA" publisher="Springer, Cham" pageNum="97-114" link="https://doi.org/10.1007/978-3-030-55754-6_6"}

::ref-item{type="book" id="ramachandran" authors="Muthu Ramachandran" title="Engineering Ethics of AI by Design" chapter="Case Studies in AI Ethics" year="2025" publisher="Springer, Singapore" pageNum="193-229" link="https://doi.org/10.1007/978-981-95-2909-4_5"}

## Outline

:::{.outline}

1. Introduction
   1. Growing reliance on AI in high‑stakes domains (healthcare, hiring, transportation).
   2. Automated awareness mechanisms (monitoring, anomaly detection, drift detection) are powerful but limited.
   3. AI systems frequently produce inaccurate or unfair outputs that require human oversight :ref[langer].
   4. Thesis statement:

      > Human oversight remains indispensable for safe AI because awareness mechanisms alone cannot reliably detect unfairness, contextual errors, or ethically significant harms, making human judgment a necessary complement to automated monitoring.

2. Background: Awareness Mechanisms in Modern AI
   1. Definition of engineered awareness: continuous monitoring, anomaly detection, drift detection, & automated alerts.
   2. Strengths: speed, scale, consistency.
   3. Limitations:
      1. Cannot reliably detect unfairness or ethical harms :ref[langer].
      2. Cannot interpret contextual nuance or value‑laden situations :ref[hwang].
      3. Cannot be held responsible for outcomes w/ moral implications/criminal impact :ref[hwang].
   4. Why these limitations matter for safety & governance.

3. The Role of Human Oversight
   1. Forms of oversight: human‑in‑the‑loop, on‑the‑loop, post‑hoc review.
   2. Unique human capabilities: contextual reasoning, ethical judgment, detection of subtle harms :ref[hwang].
   3. Oversight is mandated in major governance frameworks (e.g., EU AI Act).
   4. Oversight is expected to reliably reduce risks associated with AI systems :ref[langer].
   5. To illustrate the importance of human oversight & discuss how & where it helps, the following case studies will be considered throughout the rest of the paper:
      1. **Case study #1:** _on hiring biases at Amazon_:ref[ramachandran]

         Amazon created an internal AI tool to automatically score and rank job applicants for technical roles.
         The model was trained on 10 years of historical resumes from Amazon’s engineering hires.
         Because Amazon’s engineering workforce was overwhelmingly male, the training data encoded:
         - historical gender imbalance
         - biased hiring patterns
         - male‑associated career trajectories

         The model learned these patterns as if they were signals of merit.

      2. **Case study #2:** _on Uber self-driving car crash_:ref[ramachandran]

         _Failure: Automated awareness failed to detect gender bias in training data._
         - A self‑driving Uber test vehicle struck and killed a pedestrian in Tempe, Arizona.
         - The vehicle’s perception system misclassified the pedestrian multiple times.
         - The system’s emergency braking was disabled during autonomous mode.
         - A human "safety driver" was supposed to intervene, but she was distracted.
         - No one, human or machine, recognized the danger in time.

4. Where Automated Awareness Fails
   1. Types of failures automated systems struggle to detect:
      1. Unfair outputs (e.g., discriminatory decisions) :ref[langer].
      2. Contextual errors requiring domain knowledge :ref[hwang].
      3. Ethically significant harms that require human value judgments :ref[hwang].
   2. Why these failures require human interpretation.
   3. Real‑world examples referenced in oversight literature (e.g., misclassifications, rights violations).
      1. **Case study #1:** _on hiring biases at Amazon_:ref[ramachandran]

         The model learned to:
         - downgrade resumes containing terms like "women’s chess club"
         - penalize graduates from women’s colleges
         - reward male‑associated language and career paths

         Even after engineers removed explicit gender markers, the model continued discriminating through proxy variables, such as:
         - extracurriculars
         - word choice
         - job titles
         - career gaps
         - college names

         This is a classic example of latent bias extraction; where the model reconstructs protected attributes from correlated features. Automated awareness failed to catch this bias because the system had no internal mechanism to detect:
         - biased correlations
         - discriminatory outcomes
         - harm to protected groups
         - violations of fairness norms
         - proxy variables encoding gender

         This is exactly the kind of failure Langer, Baum & Schlicker describe: automated systems cannot detect unfairness because fairness is a human judgment, not a pattern in data:ref[langer].

      2. **Case study #2:** _on Uber self-driving car crash_:ref[ramachandran]

         The vehicle’s perception system repeatedly changed its classification of the pedestrian:
         - "Unknown object" → "Vehicle" → "Bicycle"
         - It never stabilized on a correct classification.
         - It never predicted a collision with enough confidence to trigger action.
           The system also lacked:
         - Uncertainty awareness
         - Hazard awareness
         - Fail‑safe escalation
         - Redundant safety checks

         In other words, the AI had no internal mechanism to recognize that it was confused. This is a textbook case of automated awareness failure.

5. Why Human Oversight Is Indispensable
   1. Oversight as a safeguard against algorithmic blind spots :ref[langer].
   2. Oversight as a mechanism for accountability & legitimacy :ref[hwang].
   3. Oversight is necessary because automated systems cannot reliably detect unfairness or contextual errors :ref[langer].
   4. Human judgment complements automated monitoring in ethically charged contexts.
      1. **Case study #1:** Amazon hiring biases:ref[ramachandran].
         - only humans can define fairness
         - only humans can identify protected groups
         - only humans can interpret social context
         - only humans can recognize ethical violations

         The model was focused soley on optimizing candidate selection & didn’t "know" it was discriminating. Humans are the only agents capable of normative awareness & ethical judgement :ref[langer, hwang].

      2. **Case study #2:** _on Uber self-driving car crash_:ref[ramachandran].

         This case is a prime example of where proper human oversight could have prevented an extreme & harmful outcome of automated awareness failure.
         - Where the autmated system became confused, a human could easily recognize a pedestrian & resolve the confusion--this happens because the automated system had no way of even knowing that it _was_ confused.
         - Poor policies left the emergency braking system disabled, at the cost of a human life.

6. Challenges & Limitations of Human Oversight
   1. Cognitive constraints & error‑detection limits (signal detection perspective) :ref[langer].
   2. Automation bias & over‑trust in AI outputs :ref[langer].
   3. Difficulty interpreting system behavior in real time :ref[hwang].
   4. Feasibility issues in high‑speed or high‑complexity systems (e.g., autonomous vehicles) :ref[hwang].
   5. These limitations do not negate the need for oversight but highlight the need for better design.
      1. **Case study #1:** Amazon hiring biases:ref[ramachandran].

         Humans reviewed the system’s outputs, but:
         - the rankings looked "reasonable"
         - the bias was statistical, not obvious
         - reviewers lacked tools to inspect model logic
         - no fairness dashboards existed
         - no one defined a fairness standard
         - humans trusted the system because it was "data‑driven"

         This is a strong example of **oversight impossibility**; where humans cannot detect harms they cannot see. This accurred in the Amazon hiring case because the model is a black box, reviewers were not trained in fairness auditing, & the system _appeared_ objective.

      2. **Case study #2:** _on Uber self-driving car crash_:ref[ramachandran].

         Uber’s design assumed: "If the AI fails, the human will catch it."

         But the human was placed in an impossible role:
         - She had to monitor a system that usually worked.
         - She had no real‑time feedback about the AI’s uncertainty.
         - She was supervising a task that required millisecond‑level reaction time.
         - She was expected to intervene only in rare emergencies.

         Humans are not cognitively equipped for this kind of vigilance. This is exactly what Langer, Baum & Schlicker describe: humans supervising automation experience vigilance decay, overtrust, and slow reaction times.

7. Designing Effective Hybrid Oversight Systems
   1. Principles for integrating human judgment with automated awareness.
   2. Metrics & monitoring to support oversight (real‑time correctness assurance) :ref[gubkin, phan].
   3. Exception management workflows & escalation pathways :ref[phan].
   4. Training, calibration, & interface design to improve oversight quality.
   5. Balancing simple checklists with context‑sensitive empirical testing.

8. Implications for AI Safety, Governance, & Ethics
   1. Oversight as a requirement in high‑risk AI systems (e.g., EU AI Act).
   2. Organizational responsibility & liability :ref[hwang].
   3. Ethical obligations in deploying AI systems that affect rights & well‑being :ref[hwang].
   4. The future of hybrid human‑AI decision systems.

9. Conclusion
   1. Restate the thesis.
   2. Summarize why human oversight remains essential.
   3. Emphasize the need for hybrid systems combining automated awareness with human judgment.
   4. Close with a reflection on building safe, trustworthy AI

:::

## literature review

In the above outline, 5 sources are referenced (in order of appearance). Below, each source is quickly summarized & ways in which it might be useful are discussed.

### 1. Langer et al. (2025). "Effective Human Oversight of AI‑Based Systems":ref[langer]

The authors argue that effective human oversight—as required by legislation like the EU AI Act—depends fundamentally on humans’ ability to detect errors in AI systems. Errors include both:

- Inaccuracies (wrong predictions, misclassifications)
- Unfairness (outputs violating fairness standards)

They propose Signal Detection Theory (SDT) as a rigorous framework for understanding and measuring how well humans detect such errors.

#### How it will be used

Signal Detection theory is itself a useful idea for reasoning about & designing AI systems. Additionally, Langer et al identify some key areas in which humans & automated systems contribute to engineering awareness in AI&mdash;and some critical flaws in their awareness cabilities too.

### 2. Hwang (2024). "Ethics of artificial intelligence: examining moral accountability in autonomous decision‑making systems":ref[hwang]

The paper investigates moral accountability in autonomous AI systems, focusing on how traditional ethical theories fail to fully address responsibility when AI makes decisions without human oversight. It highlights the tension between algorithmic decision‑making and human moral responsibility, especially in high‑stakes domains like healthcare, finance, transportation, and military systems.

#### How it will be used

This source discusses some philisophical frameworks for reasoning about ethics in AI decision making & awareness. Additionally, it is useful for exploring gaps in laws regarding AI & real harms that arise from AI usage. Finally, it aids in identifying some ways to mitigate these harms.

### 3. Ramachandran (2025). "Case Studies in AI Ethics":ref[ramachandran]

A chapter of a larger work, _Engineering Ethics of AI by Design_, "Case Studies in AI Ethics" presents six major case studies illustrating how ethical failures emerge in real AI deployments. It connects each case to broader themes: bias, privacy, accountability, governance, and human oversight.

#### How it will be used

The primary use of the source is for the two main case studies:

1. Hiring bias in AI-powered candidate selection @ Amazon
2. Fatality in Uber automated vehicle crash

### 4. Gubkin (2025). "Comprehensive evaluation metrics for ai observability":ref[gubkin]

Context: A practical industry‑focused guide on how to measure, monitor, and secure AI systems in production, with emphasis on LLMs and enterprise observability platforms.

The article argues that AI systems require deeper, more specialized observability than traditional software because they fail in different ways: hallucinations, prompt injections, data leakage, drift, and unpredictable behavior.

#### How it will be used

This source is more technical & applied than the others. It will be most useful when exploring real techniques that can be used to implement some of the engineering awareness techniques discussed in the other sources.

### 5. Phan et al. (2020). "Neural simplex architecture":ref[phan]

The paper introduces the Neural Simplex Architecture (NSA) — a modernized, AI‑compatible version of the classic Simplex Architecture for runtime assurance. NSA provides formal safety guarantees for systems controlled by neural networks (e.g., RL agents) while still allowing high performance.

#### How it will be used

While an older source in the fast-paced world of AI, Phan's work on NSA is foundational for exploring how automated systems can be made better, allowing them to overcome issues where only human oversight could correct themm before. By studying this work, I hope to examine some case studies & outcomes that can be achieved through new system designs in AI decision making, exception handling, & awareness loops.

::ref-list
