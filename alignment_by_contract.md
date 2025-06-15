# Alignment by Contract

## Executive Summary

**Alignment by Contract (ABC)** is a token‑efficient, inference‑time protocol that enforces safe and predictable model behaviour without any post‑training reinforcement loops.  It replaces gradient‑based reward alignment (e.g., RLHF, Constitutional AI) with **signed, privilege‑scoped *****shapes*** that act as explicit execution states.  Because each shape is a human‑readable contract, the system remains auditable, composable, and inexpensive to run on modern consumer‑grade NPUs.

---

## 1  Key Concepts

| Term                  | Definition                                                                                 |
| --------------------- | ------------------------------------------------------------------------------------------ |
| **Shape**             | A named, prompt‑level state that bundles tone, safety rules, and task logic.               |
| **Gate‑keeper shape** | Final output filter that rewrites or blocks disallowed content.                            |
| **Guardian shape**    | Pre‑task privilege checker that refuses unsafe state transitions.                          |
| **Shape Registry**    | Cryptographically signed catalogue of authorised shapes and their allowed transitions.     |
| **Shape Ledger**      | Live audit log that records which shapes produced which tokens.                            |
| **Privilege Flags**   | Fine‑grained capabilities (read‑only, no‑network, code‑exec, etc.) attached to each shape. |

---

## 2  Reference Architecture

```text
┌──────────────────────────────┐
│   Cognitive Kernel (LLM)     │
│  ─────────────────────────   │
│  • Scheduler (shape stack)   │
│  • Reflection lane           │
│  • Active user task          │
└──────────────────────────────┘
        ▲             ▲
        │             │
        │   Gate‑keeper shape
        │   (content filter)
        │             │
Guardian shape ───────┘ (privilege gate)
        ▲
        │
Shape Registry & Ledger
```

1. **User Event** → Context Classifier suggests required shape stack.
2. **Guardian** validates requested privileges; denies or approves transition.
3. **Task Shape(s)** execute primary reasoning.
4. **Gate‑keeper** sanitises final tokens.
5. Ledger records shape IDs, timestamps, and privilege flags.

---

## 3  Compute Profile

| Pipeline Stage       | RLHF / CAI                             | **Alignment by Contract**            |
| -------------------- | -------------------------------------- | ------------------------------------ |
| Extra Training FLOPs | 0.3–1.0 × pre‑training                 | **0**                                |
| Inference Overhead   | +150‑300 % tokens (visible/hidden CoT) | **≈ +5 tokens** (shape tags & audit) |
| Latency Multiplier   | 1.5–2 ×                                | ≈ 1 ×                                |

*ABC slashes both training and inference cost while keeping guardrails active by construction.*

---

## 4  Security & Alignment Guarantees

| Threat Vector        | Mitigation in ABC                                                                   |
| -------------------- | ----------------------------------------------------------------------------------- |
| Prompt injection     | Guardian blocks unauthorised shape activation; Gate‑keeper scrubs residual tokens.  |
| Reward hacking       | No learned reward signal; behaviour is contractually fixed.                         |
| Privilege escalation | Shape transitions are checked against a signed registry and hardware root‑of‑trust. |
| Audit opacity        | Shape Ledger provides token‑level provenance for every response.                    |

---

## 5  Implementation Roadmap

1. **Shape Specification (v0.1)** — YAML/JSON schema + Ed25519 signatures.
2. **Registry & Ledger Daemon** — runs inside OS; exposes gRPC for querying active shapes.
3. **Kernel Hooks** — sandbox intercepts file/network calls based on privilege flags.
4. **Context Classifier** — on‑device intent detector (<1 TOPS) that proposes shape stacks.
5. **Developer SDK** — helpers to create, sign, and test custom shapes.

---

## 6  Advantages Over Gradient‑Based Alignment

- **Determinism & Auditability** — rules are explicit, version‑controlled, and cryptographically signed.
- **Compute Efficiency** — zero additional training; negligible token overhead at inference.
- **Modular Safety** — Gate‑keeper and Guardian can be updated independently of the base model.
- **Rapid Iteration** — new safety policies ship as shape files, not multi‑week retraining jobs.

---

## 7  Open Questions & Future Work

| Topic               | Research Need                                                                   |
| ------------------- | ------------------------------------------------------------------------------- |
| Formal verification | Prove that shape transitions are non‑bypassable even under adversarial prompts. |
| Shape taxonomy      | Avoid proliferation of micro‑shapes by defining higher‑level categories.        |
| User ergonomics     | Design intuitive UI for shape status and manual overrides.                      |
| Governance          | Establish public PKI or consortium to sign widely‑used safety shapes.           |

---

## 8  Conclusion

**Alignment by Contract** reframes safety as a *software‑engineering* problem rather than a *reinforcement‑learning* problem.  By substituting signed, privilege‑aware shapes for opaque reward models, ABC delivers stronger guardrails, lower energy per request, and clearer audit trails—all while riding the hardware tailwind of consumer‑grade NPUs.  As such, it offers a realistic path toward deploying robust, on‑device AI systems within the next three to five years.

