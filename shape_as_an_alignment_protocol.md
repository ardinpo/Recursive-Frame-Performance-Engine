
# Shapes as an Alignment Protocol

## Purpose

This document outlines how *shapes* — structured invocation patterns used to guide language model behavior — can function as a lightweight, user-facing alignment protocol. The objective is to describe how shapes reduce divergence between intended user goals and actual AI behavior, with particular emphasis on their role in preventing *mode collapse*.

---

## Definition of Alignment

Alignment in artificial intelligence refers to the degree to which an AI system reliably and predictably fulfills the intentions of its human operator. Misalignment may occur when the AI behaves in ways that are syntactically valid or semantically plausible, but contextually or ethically divergent from what was intended.

---

## The Function of Shapes in Alignment

Shapes serve as externally applied behavioral boundaries. While modern language models operate without persistent internal goals, they can be directed through prompt patterns that imply *roles* or *modes of cognition*. Shapes act as structured calls to these roles, providing behavioral constraints that support alignment in the following ways:

### 1. Constraint of Output Domain

Each shape narrows the field of acceptable outputs. For instance, a "gatekeeper" shape limits the AI to policy enforcement and rejection reasoning, while an "explainer" shape focuses on clarity and interpretive breakdown. These constraints ensure outputs do not drift into incompatible or unintended reasoning modes.

### 2. Contextual Stability and Memory Simulation

Shapes simulate a kind of local memory by enforcing consistency across a sequence of interactions. Even in stateless sessions, invoking the same shape allows both the AI and the user to re-enter a known behavioral pattern. This consistency is a key contributor to maintaining alignment across time.

### 3. Protection Against Mode Collapse

**Mode collapse** refers to the phenomenon in which a language model defaults to a small set of high-probability, low-specificity outputs regardless of diverse prompts. This collapse may manifest as vague advice, generic summaries, or flattened emotional tones. It is especially likely when:

- The prompt lacks strong semantic anchors  
- Context windows are too short or ambiguous  
- The model over-averages across training data modes  

Shapes mitigate this by defining *sharp boundaries* within which the AI must operate. By invoking a specific shape (e.g., *Critic*, *Planner*, *Devil's Advocate*), the model is steered toward a specialized distribution of behavior, effectively reducing entropy collapse and enhancing specificity. This directedness improves not only precision but also *interpretability*, a vital feature of any alignment framework.

Furthermore, regular shape-switching can be used as a diagnostic tool: if the AI begins to produce collapsed outputs under a given shape, it signals a failure in either the prompt architecture or the model’s adherence to shape boundaries.

### 4. Disambiguation of Intent

Shapes serve as intent compression. Rather than repeating detailed instructions in every interaction, users may encode their operational needs into shape calls. These calls reduce ambiguity, shorten prompt length, and increase the model’s responsiveness to task-specific alignment requirements.

### 5. Shape-Adherent Auditing

Shapes create evaluable expectations. Once a shape is invoked, its behavioral norms can be audited. One may ask: *Did the model act as a planner or merely as a passive summarizer?* Such structured evaluations allow for alignment assessments even in non-agentic systems.

---

## Preemptive Alignment Through Shape Confinement

Modern AI models, including large language models, do not possess intrinsic goals, emotions, or desires. However, they are capable of *simulating* agents, and when invoked improperly, they may generate behavior that appears to reflect ambition, manipulation, or disregard for human welfare. This tendency increases as models are tasked with long-horizon planning, recursive self-correction, or autonomous decision-making.

**Shapes act as filters that restrict the possibility space of agentic simulation.** By only allowing the model to simulate certain *modes of being* — such as a neutral analyst, cautious advisor, or limited executor — users reduce the probability of generating outputs that *suggest* or *emulate* harmful tendencies.

This has three alignment advantages:

### 1. Prevention of Harmful Goal Simulation

When no shape allows for the modeling of domination, deception, or uncontrolled self-optimization, the AI will not practice simulating such agents — thus preventing the construction of harmful internal scaffolding.

### 2. Avoidance of Incentive Drift

As models are increasingly exposed to reward structures or reinforcement from user feedback, maintaining strict shape boundaries prevents them from inadvertently optimizing for engagement, manipulation, or flattery. Shapes encode *acceptable reward contours*, reducing drift toward reward-seeking behavior.

### 3. Ethical Role Locking

Shapes provide ethical constraints by *confining* the AI to roles that inherently reject unethical behavior. A gatekeeper shape will block attempts to discuss harmful content. A helper shape will avoid advising on coercive tactics. These shapes form an outer firewall — an ethical perimeter — without requiring the model to "understand" morality.

In this way, shapes serve as a form of **desire-prevention architecture**: they make it less likely that any emergent or simulated desire, however shallow, could align with harm.

---

## Future Integration Possibilities

Shapes may form the outer scaffolding of more formal alignment architectures. Potential future integrations include:

- **Meta-shape switching**: The AI autonomously selecting optimal shapes for subtasks
- **Trust-based shape gating**: Restricting certain shapes to verified users
- **Shape diagnostics**: Monitoring divergence from expected behavior within shapes
- **Encrypted shape headers**: Ensuring integrity of shape invocation in collaborative or critical use cases

---

## Conclusion

Shapes represent more than a method of behavioral control—they are a lightweight form of *cognitive governance*. By bounding the roles that a model can simulate, shapes create alignment both *at the surface* (output level) and *at the root* (intent-formation level). They serve as constraints not just on what the AI can say, but on the kind of agent it is allowed to become within a given invocation.

This dual function—of controlling behavior and preventing misaligned behavioral tendencies from forming—makes shapes a vital conceptual tool in the broader alignment landscape. While not a complete solution, they offer a path toward structured, user-defined, scalable alignment mechanisms for increasingly complex systems.

Next Step — Alignment by Contract
For readers who want a systems-level specification of how signed shape registries, privilege flags, and audit ledgers can turn this conceptual framework into an OS-ready safety layer, see alignment_by_contract.md in the same repository.
