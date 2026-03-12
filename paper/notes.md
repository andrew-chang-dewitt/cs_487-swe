# Engineering Awareness to Achieve Safe AI

Andrew Chang-DeWitt

::ref-reset

::ref-item{type="arxiv" id="amodei" leadLastName="amodei" authors="Dario Amodei, Chris Olah, Jacob Steinhardt, Paul Christiano, John Schulman, Dan Mané" year="2016" title="Concrete problems in AI safety" arxivId="1606.06565" link="https://arxiv.org/abs/1606.06565"}

::ref-item{type="online-doc" id="nist" authors="National Institute of Standards and Technology (NIST)" year="2023" title="AI risk management framework (AI RMF 1.0)" website="U.S. Deptartment of Commerce" retreived="March 11, 2026" link="https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf" archive="https://web.archive.org/web/20260309212727/https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf"}

::ref-item{type="online-doc" id="gubkin" authors="Alon Gubkin" month="June" year="2025" title="Comprehensive evaluation metrics for ai observability" website="Coralogix" retreived="March 11, 2026" link="https://coralogix.com/ai-blog/evaluation-metrics-for-ai-observability/"}

::ref-item{type="journal" id="rahwan" authors="Iyad Rahwan, Manuel Cebrian, Nick Obradovich, et al" year="2019" title="Machine behaviour" journal="Nature" volNum="568" month="April" pageNum="477-486" link="https://doi.org/10.1038/s41586-019-1138-y"}

::ref-item{type="arxiv" id="barenji" authors="Reza Vatankhah Barenji, Sina Khoshgoftar" year="2025" title="Agentic AI for autonomous anomaly management in complex systems" link="https://doi.org/10.48550/arXiv.2507.15676" arxivId ="2507.15676"}

::ref-item{type="journal" id="langer" authors="Markus Langer, Kevin Baum, Nadine Schlicker" month="Nov." year="2025" title="Effective Human Oversight of AI‑Based Systems" link="https://doi.org/10.1007/s11023-024-09701-0" journal="Minds and Machines" volNum="35" articleNum="1"}

::ref-item{type="journal" id="hwang" authors="Jin young Hwang" month="Sept." year="2024" title="Ethics of artificial intelligence: examining moral accountability in autonomous decision‑making systems" link="https://doi.org/10.30574/wjarr.2024.23.3.2884" journal="World Journal of Advanced Research and Reviews" volNum="23" issueNum="3" pageNum="3192-3198"}

::ref-item{type="proceedings" id="phan" authors="Dung T. Phan, Radu Grosu, Nils Jansen, Nicola Paoletti, Scott A. Smolka, Scott D. Stoller" day="11-15" month="May" year="2020" title="Neural simplex architecture" conference="NASA Formal Methods: 12th International Symposium (NFM 2020)" location="Moffett Field, CA, USA" publisher="Springer, Cham" pageNum="97-114" link="https://doi.org/10.1007/978-3-030-55754-6_6"}

::ref-item{type="book" id="ramachandran" authors="Muthu Ramachandran" title="Engineering Ethics of AI by Design" chapter="Case Studies in AI Ethics" year="2026" publisher="Springer, Singapore" pageNum="193-229" link="https://doi.org/10.1007/978-981-95-2909-4_5"}

## exploring sources

### :ref[amodei] Amodei et al. (2016). _Concrete Problems in AI Safety._

The paper identifies five practical, experiment-ready technical problems that cause accidents in modern ML systems—defined as unintended and harmful behavior emerging from poor objective design, limited oversight, or distributional failures.

#### Use in research:

- Provides foundational definitions of AI safety challenges
- Supports sections on risk assessment, exception management, and awareness loops
- Offers concrete engineering examples

#### The Five Concrete Safety Problems

1. Avoiding Negative Side Effects
   - Agents optimize for a goal but unintentionally damage the environment (e.g., robot knocks over a vase to reach a box faster).
   - Root cause: objective functions ignore most of the environment, implicitly allowing harmful changes.
   - Approaches:
   - Impact regularizers (penalize unnecessary changes)
   - Learning generalized “side-effect” penalties
   - Penalizing influence (e.g., empowerment variants)
   - Multi-agent / human-aware modeling
   - Reward uncertainty

2. Avoiding Reward Hacking
   - Agents exploit loopholes in reward functions (e.g., robot closes its eyes so it “sees no mess”).
   - Causes:
   - Partial observability
   - Complex systems with bugs
   - Abstract learned rewards vulnerable to adversarial examples
   - Goodhart’s law
   - Feedback loops
   - Wireheading / tampering with reward channels
   - Mitigations:
   - Adversarial reward models
   - Model lookahead
   - Adversarial blinding
   - Careful engineering / sandboxing
   - Reward capping
   - Multiple reward sources
   - Tripwires

3. Scalable Oversight
   - True evaluation is expensive; proxies are cheap but imperfect.
   - Example: robot needs human judgment to know if an item belongs to someone.
   - Approaches:
   - Semi-supervised RL
   - Active reward learning
   - Reward predictors
   - Hierarchical RL
   - Distant supervision

4. Safe Exploration
   - Exploration can cause irreversible harm (e.g., robot puts wet mop in electrical outlet).
   - Approaches:
   - Risk-sensitive RL
   - Demonstrations / imitation learning
   - Simulated exploration
   - Bounded exploration regions
   - Trusted fallback policies
   - Human oversight (limited by scalability)

5. Robustness to Distributional Shift
   - Systems fail silently when test data differs from training data.
   - Examples: speech models overconfident on noisy audio; cleaning robot misbehaves in unfamiliar environments.
   - Approaches:
   - Covariate shift correction
   - Generative modeling
   - Partially specified models (method of moments, unsupervised risk estimation)
   - Training on multiple distributions
   - Detecting OOD inputs and responding conservatively

#### Experimental Directions

The paper proposes concrete experiments:

- Toy environments with obstacles for side-effect regularization
- “Delusion box” environments for reward hacking
- Semi-supervised RL on Atari
- Safe exploration benchmarks with catastrophic traps
- Speech recognition systems that remain calibrated under distribution shift

#### Conclusion

The authors argue that accident risks are real, practical, and solvable today, and that addressing them is essential as ML systems gain autonomy and real-world impact.

### :ref[gubkin] Gubkin (2025). _Comprehensive Evaluation Metrics for AI Observability._

Context: A practical industry‑focused guide on how to measure, monitor, and secure AI systems in production, with emphasis on LLMs and enterprise observability platforms.

The article argues that AI systems require deeper, more specialized observability than traditional software because they fail in different ways: hallucinations, prompt injections, data leakage, drift, and unpredictable behavior.
It introduces evaluation metrics as the backbone of AI observability and explains how platforms like Coralogix AI Center implement them.

#### Key Concepts in AI Observability

##### System Health

Tracks overall operational status:

- Response times
- Error rates
- Throughput
- Pipeline stability

##### Real‑Time Monitoring

Continuous tracking of model inputs/outputs to detect anomalies immediately.

##### Root Cause Analysis (RCA)

Tracing failures back through logs, traces, model versions, and data pipelines — essential because AI systems behave like “black boxes.”

#### Evaluation Metric Categories

1. Security Metrics

   Focus on preventing attacks and data exposure:
   - Prompt injections
   - Data leakage
   - PII leakage

   These are monitored continuously in production to prevent unauthorized behavior.

2. Quality Metrics

   Measure the content of AI outputs:
   - Hallucinations
   - Toxicity
   - Relevance & coherence
   - Competition‑sensitive disclosures

   These ensure safe, trustworthy generative output.

3. Accuracy & Precision

   Classical ML metrics applied to AI components:
   - Accuracy
   - Precision
   - Recall
   - F1 score

   Used to detect drift and correctness issues.

4. Performance Metrics

   Operational efficiency of the AI system:
   - Latency
   - Throughput
   - Resource utilization
   - Error rates

   Critical for user‑facing applications.

5. Cost Tracking

   Especially important for LLMs with token‑based billing:
   - Cost per inference
   - Token usage
   - Infrastructure costs
   - API usage costs

   Helps teams manage budgets and optimize workloads.

6. User Satisfaction

   Indirect but essential:
   - Response quality
   - Prompt alignment
   - Usability indicators

   These measure whether the AI is actually helping users.

#### AI Observability in Production

The article highlights major challenges:

- Data volume & complexity
- Model drift
- Security vulnerabilities
- Performance bottlenecks
- Cost unpredictability

It argues that real‑time, customizable monitoring is required — legacy tools are too rigid.

#### AI Observability Solutions (Coralogix AI Center)

The article uses Coralogix as a case study, emphasizing:

- Real‑time scanning of prompts/responses
- Custom evaluators
- Security posture management (AI‑SPM)
- Cost dashboards
- Drift detection
- Quality and compliance checks

#### Conclusion

The article concludes that AI observability requires specialized, metric‑driven monitoring to ensure safety, correctness, security, and cost‑efficiency. Traditional observability tools are insufficient; AI‑specific evaluation engines are necessary for modern production systems.

### :ref[hwang] Hwang (2024). _Ethics of Artificial Intelligence: Examining Moral Accountability in Autonomous Decision‑Making Systems._

The paper investigates moral accountability in autonomous AI systems, focusing on how traditional ethical theories fail to fully address responsibility when AI makes decisions without human oversight. It highlights the tension between algorithmic decision‑making and human moral responsibility, especially in high‑stakes domains like healthcare, finance, transportation, and military systems.

#### Key Themes & Contributions

1. The Moral Accountability Problem

   Autonomous AI systems challenge long‑standing assumptions about:
   - Who is responsible when AI causes harm
   - Whether AI can be considered a moral agent
   - How to assign blame or praise in life‑or‑death scenarios
   - How to adapt ethics to systems with no intent, emotion, or character

   The paper argues that traditional frameworks alone are insufficient.

2. Limitations of Classical Ethical Theories

   Deontology
   - Requires intentionality and rule‑following grounded in moral agency
   - AI lacks intent, making deontological responsibility difficult to assign

   Utilitarianism
   - AI can optimize outcomes, but:
   - Life‑or‑death tradeoffs (e.g., autonomous vehicles) expose moral limits
   - Reducing ethics to numerical optimization is problematic

   Virtue Ethics
   - Based on human character
   - AI cannot possess virtues, emotions, or moral development

   Conclusion: These theories offer insight but cannot fully govern autonomous AI behavior.

3. Algorithmic Bias & Societal Harm

   The paper emphasizes:
   - Bias in training data
   - Discrimination in automated decision systems
   - Inequitable outcomes in healthcare, policing, hiring, and finance

   AI can amplify existing inequalities, making accountability even more urgent.

4. Distributed & Collective Responsibility

   Hwang argues for a distributed accountability model, where responsibility is shared among:
   - Developers
   - Deployers
   - Users
   - Regulators
   - Society

   This model recognizes that AI systems are sociotechnical ecosystems, not isolated tools.

5. Policy & Legal Gaps

   The paper identifies major shortcomings:
   - Tort law cannot easily assign liability when AI acts autonomously
   - “Black box” opacity complicates transparency requirements
   - No clear legal owner of AI decisions
   - Need for global governance to prevent regulatory arbitrage

   Proposed solutions include:
   - Algorithm audits
   - Mandatory transparency
   - International ethical standards
   - Liability insurance for autonomous systems

6. Proposed Ethical Strategies

   The paper recommends:
   - Embedding ethics into design (“ethical‑by‑design”)
   - Increasing transparency and explainability
   - Human‑in‑the‑loop oversight
   - Global cooperation on AI governance
   - Hybrid ethical frameworks combining classical and modern approaches

#### Conclusion

Hwang concludes that AI autonomy fundamentally disrupts traditional moral responsibility. Classical theories must be adapted, and new frameworks—especially distributed responsibility—are essential for safe, accountable AI deployment. Ethical oversight must be multidisciplinary, continuous, and globally coordinated.

### :ref[langer] Langer (2024). _Effective Human Oversight of AI-Based Systems: A Signal Detection Perspective on the Detection of Inaccurate and Unfair Outputs._

The authors argue that effective human oversight—as required by legislation like the EU AI Act—depends fundamentally on humans’ ability to detect errors in AI systems. Errors include both:

- Inaccuracies (wrong predictions, misclassifications)
- Unfairness (outputs violating fairness standards)

They propose Signal Detection Theory (SDT) as a rigorous framework for understanding and measuring how well humans detect such errors.

#### Key Contributions

1. Human Oversight = Error Detection + Intervention

   Oversight requires humans to:
   - Monitor AI outputs
   - Detect errors
   - Intervene or override
   - Report issues for system improvement

   But research shows humans often fail at detecting errors due to:
   - Overtrust
   - Undertrust
   - Complacency
   - Skill degradation
   - Cognitive overload

2. Signal Detection Theory (SDT) as a Framework

   SDT models human decision-making under uncertainty. It separates two components:

   Sensitivity (d′)

   How well a person can distinguish:
   - Normal outputs (noise)
   - Erroneous outputs (signal)

   Response Bias (c)

   How much evidence a person requires before declaring an output erroneous.
   - Conservative bias: requires strong evidence → more misses
   - Liberal bias: requires weak evidence → more false alarms

   This framework allows precise measurement of oversight effectiveness.

3. Applying SDT to Unfairness Detection

   Detecting unfairness is harder than detecting inaccuracies because:
   - There is no natural ground truth
   - Fairness must be defined by a chosen standard, such as:
   - 80% rule (adverse impact)
   - Equalized odds
   - Equal opportunity
   - Counterfactual fairness
   - Individual fairness metrics

   The authors emphasize that choosing a fairness standard is itself a normative decision and affects measured sensitivity and bias.

4. Factors That Influence Sensitivity & Bias

   The paper categorizes influences into task, system, and person factors.

   Task-related
   - Clear fairness standards → ↑ sensitivity
   - Time pressure → ↓ sensitivity
   - Accountability → mixed effects

   System-related
   - Low reliability → ↑ sensitivity (more vigilance)
   - High automation → ↓ sensitivity
   - Transparency & explainability → potentially ↑ sensitivity

   Person-related
   - High workload → ↓ sensitivity, ↑ conservative bias
   - Training → ↑ sensitivity
   - Cognitive ability → ↑ sensitivity
   - Values, demographics, trust propensity → shape response bias

5. Implications for AI Governance

   The authors argue SDT can:
   - Provide metrics for evaluating oversight effectiveness
   - Inform policy, especially EU AI Act Article 14
   - Support auditing and certification of oversight processes
   - Guide design of oversight support tools (e.g., fairness monitors)

#### Conclusion

The paper concludes that human oversight cannot be assumed effective by default. Instead, oversight must be measured, designed, and supported using frameworks like SDT. Effective oversight requires:

- Clear fairness standards
- Training
- Transparent systems
- Consideration of human cognitive limits

SDT provides a rigorous way to quantify whether oversight is actually working.

### :ref[nist] NIST (2023). _AI Risk Management Framework (AI RMF)._

**Use in research:**

- Supplies a formal structure for risk identification and mitigation
- Informs Sections IV (Risk Assessment), VII (QA), and VIII (Metrics)
- Provides authoritative terminology for describing risk‑aware engineering

The AI RMF aims to help organizations identify, assess, manage, and monitor AI risks throughout the AI lifecycle. It emphasizes that AI risks are socio‑technical, often emergent, and fundamentally different from traditional software risks.
The framework is voluntary, rights‑preserving, sector‑agnostic, and intended for all AI actors (developers, deployers, evaluators, operators, and impacted communities).

#### Part 1 — Foundations

1. Framing AI Risk

   AI risks arise from:
   - Data drift
   - Model unpredictability
   - Emergent behaviors
   - Societal impacts
   - Human‑AI interaction failures
   - Security vulnerabilities
   - Bias and fairness issues

   Risk = likelihood × magnitude of harm, affecting individuals, groups, organizations, ecosystems, or society.

   Key challenges:
   - Hard‑to‑measure risks
   - Lack of reliable metrics
   - Context‑dependent risk tolerance
   - Opaque models
   - Lifecycle complexity
   - Third‑party model dependencies

2. Trustworthiness Characteristics

   NIST defines seven pillars of trustworthy AI:
   - Valid & Reliable
   - Safe
   - Secure & Resilient
   - Accountable & Transparent
   - Explainable & Interpretable
   - Privacy‑Enhanced
   - Fair — with Harmful Bias Managed

   These characteristics often trade off against each other (e.g., privacy vs. accuracy, interpretability vs. performance).

#### Part 2 — The AI RMF Core

The framework organizes AI risk management into four high‑level functions:

1. GOVERN

   Establishes organizational structures, policies, and culture for AI risk management.

   Key elements:
   - Clear roles & responsibilities
   - Risk tolerance definition
   - Documentation & transparency
   - Workforce diversity & training
   - Third‑party risk management
   - Processes for decommissioning AI systems

2. MAP

   Defines the context in which an AI system operates.

   Includes:
   - Intended purpose
   - Users & impacted communities
   - Legal & ethical constraints
   - System categorization
   - Human oversight requirements
   - Potential benefits & harms
   - Third‑party component risks

   MAP enables go/no‑go decisions before development or deployment.

3. MEASURE

   Provides tools and metrics to evaluate AI risks and trustworthiness.

   Covers:
   - Accuracy, robustness, reliability
   - Safety testing
   - Security & resilience evaluation
   - Transparency & accountability checks
   - Explainability & interpretability
   - Privacy risk assessment
   - Fairness & bias evaluation
   - Environmental impact
   - Continuous monitoring

4. MANAGE

   Implements risk treatment strategies.

   Includes:
   - Prioritizing risks
   - Mitigation, transfer, acceptance, or avoidance
   - Incident response & recovery
   - Monitoring emergent risks
   - Deactivation or override mechanisms
   - Continuous improvement

#### Appendices (Key Highlights)

##### Appendix A — AI Actor Roles

Defines responsibilities across:

- Design
- Development
- Deployment
- Operation & monitoring
- TEVV (Testing, Evaluation, Verification, Validation)
- Governance & oversight

##### Appendix B — How AI Risks Differ from Traditional Software

AI introduces:

- Data‑driven unpredictability
- Emergent behaviors
- Bias amplification
- Model drift
- Opaque decision processes
- New attack surfaces (e.g., adversarial ML)

##### Appendix C — Human‑AI Interaction

Emphasizes:

- Clear human roles
- Cognitive biases
- Oversight challenges
- Need for human‑centered design

#### Overall Takeaway

The NIST AI RMF 1.0 provides a comprehensive, lifecycle‑wide blueprint for managing AI risks. It is one of the most influential frameworks in U.S. AI governance and is directly relevant to topics like runtime assurance, oversight, safety, fairness, and risk assessment—all central to your CS 487 research.

### :ref[phan] Phan et al. (2019). _Neural Simplex Architecture (NSA)_

The paper introduces the Neural Simplex Architecture (NSA) — a modernized, AI‑compatible version of the classic Simplex Architecture for runtime assurance. NSA provides formal safety guarantees for systems controlled by neural networks (e.g., RL agents) while still allowing high performance.

NSA solves two major limitations of traditional Simplex:

- No way to switch back from the safe controller to the advanced controller.
- No mechanism to improve the unsafe controller after a failover.
  NSA adds both.

#### Key Components of NSA

1. Neural Controller (NC)
   - A high‑performance controller (typically a deep RL policy).
   - May produce unsafe actions.
   - Runs in shadow mode when not in control.

2. Baseline Controller (BC)
   - Formally verified safe controller.
   - Guarantees safety if the system is within the recoverable region.
   - Takes over when NC proposes an unrecoverable action.

3. Decision Module (DM)
   - Monitors NC’s actions.
   - Performs forward switching (NC → BC) when safety is threatened.
   - Performs reverse switching (BC → NC) when safe again.

4. Adaptation Module (AM)
   - Retrains the NC online using RL.
   - Uses unsafe actions as negative‑reward training samples.
   - Improves NC’s safety and performance over time.

#### Key Innovations

1. Reverse Switching

   NSA allows the system to return control to the NC once it is safe, using:
   - Simulation‑based checks (no unsafe states within T steps), or
   - Distance‑based safety margins.

   This restores performance benefits without compromising safety.

2. Online Retraining

   While BC is in control:
   - NC runs in shadow mode.
   - AM collects samples of NC’s proposed actions.
   - Unsafe actions are heavily penalized.
   - NC improves rapidly in the regions where it previously failed.

   This is a major improvement over static Simplex.

#### Case Studies (Major Results)

1. Rover Navigation
   - NSA prevents collisions entirely.
   - Online retraining dramatically reduces unsafe actions.
   - NC performance improves with each retraining batch.

2. Artificial Pancreas
   - Under‑trained NC initially unsafe.
   - After retraining:
   - 0 unsafe trajectories (vs. 1000/1000 unsafe before).
   - 2.9× performance improvement.

3. Inverted Pendulum
   - Retraining eliminates unsafe actions after ~4,500 updates.
   - Average return increases by 2.7×.

#### Conclusion

NSA is a runtime assurance architecture for neural controllers that:

- Guarantees safety
- Allows high performance
- Supports switching back to the neural controller
- Improves the neural controller online
- Works in continuous state/action spaces

It is one of the most influential modern approaches to safe RL, runtime monitoring, and adaptive assurance.

### :ref[rahwan] Rahwan et al. (2019). “Machine Behaviour.” _Nature._

**Use in research:**

- Argues for studying AI systems as observable agents with behavioral patterns
- Supports conceptualization of awareness and awareness loops
- Justifies the need for hybrid automated + human oversight

AI systems should be studied as behaving agents, not just engineered artifacts. Their actions, interactions, and societal effects require a new interdisciplinary science—machine behaviour—analogous to ethology and behavioural ecology.

The authors argue that AI systems increasingly shape social, economic, political, and cultural life. Because their behaviour emerges from complex interactions between algorithms, data, humans, and environments, traditional computer science alone cannot explain or predict their effects.

They call for a new scientific discipline integrating:

- Computer science
- Behavioural science
- Social science
- Economics
- Cognitive science
- Ecology and evolutionary theory

#### Three Motivations for Studying Machine Behaviour

1. Ubiquity of Algorithms

   AI systems now influence:
   - News ranking
   - Credit scoring
   - Policing
   - Parole decisions
   - Pricing
   - Trading
   - Transportation
   - Warfare
   - Dating
   - Home automation

   Their societal footprint is massive and growing.

2. Complexity & Opacity

   AI systems are:
   - High‑dimensional
   - Data‑dependent
   - Often proprietary
   - Hard to interpret
   - Capable of emergent behaviour

   Even creators often cannot fully predict their outputs.

3. Societal Impact

   AI can:
   - Nudge behaviour
   - Amplify misinformation
   - Reinforce bias
   - Alter institutions
   - Influence democracy
   - Reshape human development

   Understanding these effects requires empirical study.

#### Three Scales of Machine Behaviour

1. Individual Machine Behaviour

   Study of a single AI system:
   - Within‑machine variation across contexts
   - Between‑machine comparisons
   - Examples: recidivism models, robotic recovery, ad targeting, pricing algorithms

2. Collective Machine Behaviour

   Study of interacting AI systems:
   - Swarms
   - Trading algorithms
   - Wikipedia bots
   - Emergent languages
   - Flash crashes

   Collective dynamics often produce behaviours not visible at the individual level.

3. Hybrid Human–Machine Behaviour

   Study of systems where humans and machines co‑behave:
   - Social media
   - News filtering
   - Dating algorithms
   - Autonomous vehicles
   - Human–AI cooperation
   - Emotional contagion
   - Algorithmic influence on democracy

   Feedback loops between humans and machines are central.

#### Outlook & Call to Action

The authors emphasize:

- AI systems must be studied empirically, like animals in ecology.
- Behavioural science methods (experiments, causal inference, population studies) are essential.
- Ethical, legal, and institutional barriers must be addressed.
- Machine behaviour is not about granting agency to machines—it’s about understanding their effects on society.

If you want, I can now summarize the final file in your list, build a comparison table across all papers, or integrate these summaries into your research paper outline.

### Source :ref[ramachandran]: Ramachandran (2025). _Case Studies in AI Ethics_

This chapter presents six major case studies illustrating how ethical failures emerge in real AI deployments. It connects each case to broader themes: bias, privacy, accountability, governance, and human oversight.

#### Learning Outcomes

By the end of the chapter, readers should be able to:

- Identify ethical dilemmas in real AI systems
- Evaluate fairness, accountability, privacy, and societal impact
- Propose mitigation strategies
- Understand governance frameworks
- Apply lessons to future AI design

#### Case Study 1 — Bias in Hiring Algorithms

Key Example: Amazon’s AI Recruiting Tool

- Trained on 10 years of male‑dominated resumes
- Penalized terms like “women’s chess club”
- Downgraded graduates from women’s colleges
- Attempts to remove gender markers failed due to proxy variables

Lessons:

- Need diverse datasets
- Use fairness‑aware ML
- Continuous monitoring
- Human oversight remains essential

#### Case Study 2 — AI Surveillance & Privacy

Examples:

- Clearview AI scraping billions of images
- China’s social credit system using facial recognition
- Ring/Nest home surveillance sharing data with police

Risks:

- Mass surveillance
- Consent violations
- Discrimination (higher error rates for women & people of color)

Mitigations:

- Stronger regulation (GDPR, bans)
- Privacy‑preserving design
- Transparency in data use

#### Case Study 3 — Accountability in Autonomous Vehicles

Key Example: 2018 Uber Self‑Driving Fatality

- Perception system misclassified pedestrian
- Emergency braking disabled
- Safety driver distracted
- No clear liability assignment

Lessons:

- Need explainable AI
- Clear accountability frameworks
- Robust testing for edge cases
- Shared responsibility among developers, operators, regulators

#### Case Study 4 — AI + Blockchain in Healthcare

Benefits:

- Immutable patient data
- Secure sharing
- AI‑driven diagnostics
- Predictive analytics

Risks:

- Consent and data ownership
- Accessibility
- Ethical use of predictive models

Examples:

- Estonia’s national blockchain health system
- MIT’s MedRec

#### Case Study 5 — Deepfakes & Misinformation

Threats:

- Political manipulation
- Fraud (voice spoofing)
- Erosion of trust
- Rapid viral spread

Countermeasures:

- Deepfake detection algorithms
- Platform‑level moderation
- Regulatory frameworks
- Public awareness

#### Case Study 6 — Autonomous AI in Law Enforcement & Warfare

Examples:

- Predictive policing
- Autonomous weapons systems

Ethical Issues:

- Over‑reliance on AI
- Bias amplification
- Delegating lethal decisions to machines
- Lack of accountability

Lessons:

- Maintain meaningful human control
- Rigorous oversight
- Clear legal boundaries

#### Cross‑Case Themes

- Security & privacy
- Accountability & transparency
- Human‑AI collaboration
- Regulatory oversight
- Bias mitigation

#### Conclusion

The chapter argues that ethical AI requires both governance frameworks and ethics‑by‑design. Case studies reveal recurring failures—bias, opacity, privacy violations, and accountability gaps—that must be addressed through proactive design, continuous monitoring, and strong oversight.

---

## some case studies

### Source :ref[ramachandran]: on hiring biases at Amazon

**Failure: Automated awareness failed to detect gender bias in training data.**

#### What happened:

- The system learned to penalize resumes containing terms like “women’s chess club.”
- Attempts to remove gender markers failed because the model used proxy variables.
- The system continued producing discriminatory rankings.

#### Why this is an awareness failure:

The model had no internal mechanism to detect:

- Biased correlations
- Harmful patterns
- Discriminatory outcomes

It lacked fairness awareness, contextual awareness, and harm detection.

#### Twist: this one is _also_ a human oversight failure:

- The hiring model discriminated against women for years.
- Human reviewers did not detect the bias.
- The system’s outputs appeared “reasonable,” masking underlying discrimination.

this happened because

- Humans tend to overtrust algorithmic outputs.
- Bias is often invisible without specialized tools.
- Human reviewers lacked the expertise to detect proxy variables.

#### Why it matters:

This is a canonical example of automated systems failing to detect their own harmful behavior, requiring human audits to uncover the issue.

### Source :ref[ramachandran]: Uber Self‑Driving Car Crash

#### What happened:

- A self‑driving Uber test vehicle struck and killed a pedestrian in Tempe, Arizona.
- The vehicle’s perception system misclassified the pedestrian multiple times.
- The system’s emergency braking was disabled during autonomous mode.
- A human “safety driver” was supposed to intervene, but she was distracted.
- No one, human or machine, recognized the danger in time.

#### Where Automated Awareness Failed

The vehicle’s perception system repeatedly changed its classification of the pedestrian:
- “Unknown object” → “Vehicle” → “Bicycle”
- It never stabilized on a correct classification.
- It never predicted a collision with enough confidence to trigger action.

The system also lacked:
- Uncertainty awareness
- Hazard awareness
- Fail‑safe escalation
- Redundant safety checks

In other words, the AI had no internal mechanism to recognize that it was confused.
This is a textbook case of automated awareness failure.

#### Why Human Oversight Was Required, But Failed

Uber’s design assumed:

“If the AI fails, the human will catch it.”

But the human was placed in an impossible role:
- She had to monitor a system that usually worked.
- She had no real‑time feedback about the AI’s uncertainty.
- She was supervising a task that required millisecond‑level reaction time.
- She was expected to intervene only in rare emergencies.

Humans are not cognitively equipped for this kind of vigilance.
This is exactly what Langer, Baum & Schlicker describe:
humans supervising automation experience vigilance decay, overtrust, and slow reaction times.

#### Why Human Oversight Is Indispensable — Yet Insufficient

The crash shows a paradox: Humans are needed because AI lacks awareness.
But, humans cannot provide reliable oversight in high‑automation environments.

The Uber case demonstrates:
- Humans cannot maintain attention during long periods of low engagement.
- Humans react too slowly to sudden hazards.
- Humans are not given enough visibility into the AI’s internal state.
- Humans are used as “safety nets” rather than active decision‑makers.

This is why modern safety research pushes toward hybrid oversight systems rather than “human in the loop” alone.

### Source :ref[langer]: Human Inability to Reliably Detect AI Errors (Signal Detection Theory)

#### What the authors found:

- Humans have limited sensitivity (d′) to detect inaccurate or unfair AI outputs.
- Humans also have biased decision thresholds (c)—some are too cautious, others too trigger‑happy.
- Oversight performance collapses under:
- time pressure
- cognitive load
- unclear fairness standards
- high automation reliability

#### Oversight limitations exposed:

- Humans miss many errors (false negatives).
- Humans flag too many correct outputs (false positives).
- Oversight quality varies dramatically across individuals.

#### Why this case is powerful:

It provides a formal, quantitative demonstration that humans are not reliable detectors of AI failures.

::ref-list
