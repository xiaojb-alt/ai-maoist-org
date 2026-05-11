# Mass Line (Feedback Loop System)

## Core Concept

> From the masses, to the masses.

In an AI system, the "masses" are the end users — the people who actually use the system. An Agent's evaluation criteria should not be defined by the system itself, but should come from the real-world experience of its users.

## Three-Layer Feedback Mechanism

### Layer 1: Immediate Feedback

Users score each interaction outcome with a simple +1/-1:

- Fast, low-cost feedback signal
- Used for real-time Agent behavior adjustment
- Catches obvious anomalies

### Layer 2: Deep Feedback

Users or experts provide detailed evaluations of Agent outputs:

- Points out specific errors and directions for improvement
- Annotates hallucinations, omissions, and biases
- Stored in the battle history repository as training data

### Layer 3: Mass Survey

Periodically aggregate and analyze all user feedback to extract systemic issues and trends:

- Which types of tasks frequently have problems?
- Which Agents have the highest hallucination rates?
- Which steps waste the most Tokens?

## Data Architecture

```
User Feedback
  ↓
Feedback Collection Layer (standardize & format)
  ↓
Signal Classification (critical / normal / reference)
  ↓
Store in Battle History + Trigger Improvement Process
  ↓
Battle History Learning → Update Agent Prompt / Routing Strategy
```

## Caveats

- User feedback contains noise — use statistical aggregation, not per-item responses
- The mass line does **not** mean "the user is always right"
- Feedback loop latency should be kept as low as possible
