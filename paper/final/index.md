---
title: Engineering Awareness to Achieve Safe AI
meta:
  skipRenderTitle: true
  byline: Andrew Chang-DeWitt
  published: 2026-05-02T20:00-06:00
---

:::hgroup{#titlepage.titlegroup}

# Engineering awareness to achieve safe AI

Andrew Chang-DeWitt \
CS 487 - Software Engineering \
Illinois Institute of Technology \
Spring 2026

:::

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

## Introduction

Artificial intelligence is increasingly embedded in decisions that affect health, employment, mobility, and access to essential services. These systems operate at speeds and scales that exceed human capacity, which has encouraged organizations to rely on automated monitoring, anomaly detection, and drift analysis to maintain system reliability. These mechanisms provide continuous visibility into model behavior, yet they remain limited in their ability to detect harms that involve context, fairness, or ethical interpretation. Research on human oversight shows that AI systems often generate inaccurate or unfair outputs that automated tools cannot reliably identify :ref[langer]. This creates a gap between technical monitoring and the broader forms of awareness needed for safe deployment.

As organizations adopt AI systems for decisions that affect people directly, the limits of automated monitoring become more visible. Technical tools can reveal statistical irregularities, yet they cannot interpret the social meaning of those irregularities or determine when an output carries ethical weight. These gaps create situations where automated awareness is insufficient for preventing harm. Human oversight remains indispensable for safe AI because awareness mechanisms alone cannot reliably detect unfairness, contextual errors, or ethically significant harms, making human judgment a necessary complement to automated monitoring.

## Background: Awareness mechanisms in modern AI

Engineered awareness refers to the set of techniques used to monitor AI systems during operation. These include anomaly detection, drift detection, performance dashboards, and automated alerts that signal deviations from expected behavior. Such mechanisms operate continuously and can process large volumes of data with consistency. They are well suited for identifying statistical anomalies, performance degradation, or unexpected model outputs :ref[langer].

Despite these strengths, awareness mechanisms have clear limitations. They cannot reliably detect unfairness or ethical harms because these concepts require normative interpretation rather than statistical comparison :ref[langer]. They also struggle with contextual nuance, such as understanding when a technically correct output is socially inappropriate or harmful :ref[hwang]. Automated systems cannot be held responsible for decisions that carry moral or legal implications, which places responsibility on human actors :ref[hwang]. These limitations matter because AI systems increasingly operate in environments where errors can affect rights, safety, and well‑being. Awareness mechanisms provide visibility, but they do not replace the need for human judgment.

## The role of human oversight

Human oversight takes several forms, including human‑in‑the‑loop decision making, supervisory monitoring, and post‑hoc review. Each form relies on human abilities that automated systems lack, such as contextual reasoning, ethical evaluation, and recognition of subtle harms :ref[hwang]. Governance frameworks, including the EU AI Act, require oversight for high‑risk systems because it is expected to reduce the risks associated with automated decision making :ref[langer].

Two case studies illustrate the importance of oversight. The first concerns Amazon's internal hiring tool, which was created to automatically score and rank applicants for technical roles. The model was trained on ten years of historical resumes from Amazon's engineering hires, a dataset shaped by an overwhelmingly male workforce. As a result, the system absorbed patterns that reflected historical gender imbalance, biased hiring practices, and male‑associated career trajectories. These patterns were interpreted by the model as indicators of merit, which caused the model to reproduce and reinforce the same inequities it learned from :ref[ramachandran].

The second case involves the Uber self‑driving car crash in Tempe, Arizona. During testing, the vehicle struck and killed a pedestrian after its perception system repeatedly misclassified her presence. The system cycled through labels such as "unknown object," "vehicle," and "bicycle," and never produced a stable prediction of danger. Emergency braking was disabled while the vehicle operated autonomously, and the human safety driver, who was expected to intervene when needed, was distracted. Neither the automated system nor the human supervisor recognized the hazard in time to prevent the collision :ref[ramachandran].

## Where automated awareness fails

Automated awareness systems struggle with several categories of failure. They cannot detect unfair outputs because fairness depends on social norms and legal standards rather than statistical patterns :ref[langer]. They also fail to recognize contextual errors that require domain knowledge, such as understanding when a decision is inappropriate for a specific situation :ref[hwang]. Ethical harms, such as discrimination or violations of autonomy, require human interpretation and cannot be inferred from model outputs alone :ref[hwang].

The Amazon hiring case demonstrates how automated awareness can miss forms of harm that require human interpretation. The model learned to downgrade resumes containing terms such as "women's chess club," penalize graduates from women's colleges, and reward male‑associated language and career paths. Even after engineers removed explicit gender markers, the system continued to discriminate through proxy variables that included extracurriculars, word choice, job titles, career gaps, and college names. This reflects a pattern of latent bias extraction, where the model reconstructs protected attributes from correlated features. Automated monitoring did not detect these behaviors because it lacked mechanisms for identifying biased correlations, discriminatory outcomes, harm to protected groups, violations of fairness norms, or proxy variables encoding gender :ref[ramachandran]. This is exactly the kind of failure Langer, Baum & Schlicker describe: automated systems cannot detect unfairness because fairness is a human judgment, not a pattern in data :ref[langer].

The Uber crash provides a second example of automated awareness failure. The vehicle's perception system repeatedly changed its classification of the pedestrian, shifting from "unknown object" to "vehicle" to "bicycle," and never stabilizing on a correct interpretation. It also failed to predict a collision with enough confidence to trigger action. The system lacked uncertainty awareness, hazard awareness, fail‑safe escalation, and redundant safety checks. These limitations meant the AI had no internal mechanism to recognize that it was confused. The incident illustrates how automated systems can fail when they cannot interpret their own uncertainty or recognize when intervention is necessary :ref[ramachandran].

## Why human oversight is indispensable

Human oversight provides a safeguard against blind spots in automated systems :ref[langer]. It also supports accountability by ensuring that decisions with ethical or legal consequences are reviewed by agents capable of moral judgment :ref[hwang]. Automated systems cannot reliably detect unfairness or contextual errors, which makes human interpretation necessary for safe operation :ref[langer].

In the Amazon case, human oversight was the only mechanism capable of identifying the ethical issues created by the model's behavior. Fairness cannot be defined by an automated system, and only humans can determine which groups require protection or how discrimination manifests in a hiring context. The model focused entirely on optimizing candidate selection and had no awareness that it was discriminating :ref[ramachandran]. Humans are the only agents who can interpret social context, recognize when a decision violates fairness norms, and evaluate the ethical implications of an output. This reflects the broader point that normative awareness and ethical judgment remain human responsibilities [1, 2].

The Uber case shows how human oversight, if implemented properly, could have prevented a harmful outcome when automated awareness failed. A human observer can recognize a pedestrian even when a perception system is uncertain or confused. The automated system had no way to detect its own uncertainty, yet a human could have resolved the situation quickly if placed in a role that supported effective monitoring. Instead, emergency braking was disabled, and the safety driver was expected to intervene without adequate feedback or support. The incident illustrates how poor oversight design can leave humans unable to compensate for system failures, even when they possess the perceptual abilities needed to prevent harm :ref[ramachandran].

## Challenges and limitations of human oversight

Human oversight faces its own constraints. Research using Signal Detection Theory shows that humans have limited ability to detect errors, especially when errors are rare or ambiguous :ref[langer]. Automation bias can lead supervisors to trust AI outputs even when they are incorrect :ref[langer]. Humans also struggle to interpret system behavior in real time, particularly when models are opaque or operate at high speed :ref[hwang]. These challenges are amplified in complex environments such as autonomous vehicles, where reaction times must be extremely fast :ref[hwang].

The Amazon case illustrates how oversight can fail when humans lack the tools and information needed to recognize harm. Reviewers saw rankings that appeared reasonable, missing the statistically significant, but non-obvious bias. They had no visibility into the model's internal logic, no fairness dashboards, and no defined fairness standard to evaluate the system's behavior :ref[ramachandran]. The appearance of objectivity encouraged trust in the outputs, even though the underlying process was flawed. This is a strong example of _oversight impossibility_; where humans cannot detect harms they cannot see. This accurred in the Amazon hiring case because the model is a black box, reviewers were not trained in fairness auditing, & the system appeared objective.

The Uber self-driving car case shows how oversight can fail when humans are placed in roles that exceed their cognitive limits. The system design assumed "If the AI fails, the human will catch it", yet she was expected to monitor a task that usually worked without providing real‑time feedback about the system's uncertainty :ref[ramachandran]. The role required millisecond‑level reaction time during rare emergencies, which is not compatible with human attention patterns. Supervising a system that performs reliably most of the time leads to vigilance decay, overtrust, and delayed responses, a well documented outcome in oversight research[1]. These conditions made it unlikely that the safety driver could intervene effectively when the automated system misclassified the pedestrian.

## Designing effective hybrid oversight systems

Hybrid oversight systems combine automated awareness with structured human judgment, and their design benefits from techniques described in recent observability and runtime‑assurance research. Work on AI observability outlines how real‑time metrics can reveal issues such as hallucinations, prompt injections, data leakage, drift, and performance degradation, giving supervisors clearer insight into system behavior during operation :ref[gubkin]. These metrics support oversight by making correctness, security, and stability measurable rather than implicit. Research on the Neural Simplex Architecture adds another dimension by showing how automated controllers can be paired with certified fallback mechanisms that guarantee safety while still allowing high‑performance models to operate when conditions permit :ref[phan]. Together, these approaches show how automated monitoring and structured intervention pathways can be combined to support human oversight in a predictable and transparent way.

Training and calibration help supervisors understand when intervention is necessary. Interfaces should present information in ways that reduce cognitive load and support timely decision making. Simple checklists can help structure routine oversight, while empirical testing can reveal context‑specific risks that require human interpretation.

## Implications for AI safety, governance, and ethics

Oversight is a requirement for high‑risk AI systems under emerging regulatory frameworks. Organizations that deploy AI systems bear responsibility for ensuring that oversight structures are effective and that harms are addressed promptly :ref[hwang]. Ethical obligations arise when AI systems affect rights, opportunities, or well‑being, which requires organizations to consider the broader consequences of automated decisions :ref[hwang].

Hybrid human‑AI systems will continue to shape decision making in many domains. Designing these systems requires attention to accountability, transparency, and the distribution of responsibility between humans and machines.

## Conclusion

This paper has argued that human oversight remains essential for safe AI. Automated awareness mechanisms provide monitoring and detection capabilities, but they cannot interpret fairness, context, or ethical significance. Human judgment fills these gaps by evaluating harms that automated systems cannot recognize.

Safe AI requires hybrid systems that combine automated awareness with structured oversight. Building such systems involves careful design of workflows, interfaces, and metrics that support human decision making. As AI continues to influence high‑stakes decisions, the integration of human judgment will remain a central component of responsible deployment.

::ref-list
