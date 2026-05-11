# Meta Governance Layer (Political Commissar Agent)

## Why It's Needed

In a multi-Agent system, each Agent focuses only on its own local task, lacking a global perspective and quality control. Analogous to real-world organizations:

> The commander fights the battle; the commissar guards the line.

Without a commissar, an Agent system will suffer from:

- Agents cutting corners to get the task done (fabricating data, skipping steps)
- Cross-Agent error amplification — wrong information gets reinforced across multiple agents
- No "outsider" to scrutinize the reasonableness of decisions

## Design Principles

1. **Does not participate in execution** — The commissar does not write code or generate content; it only reviews
2. **Intervenes at key checkpoints** — Spot-checks before Agent output is released, before cross-Agent handoffs, and before final delivery
3. **Has veto power** — The commissar has the authority to reject low-quality output and demand rework
4. **Battle history records** — Every intervention is logged into a battle history database for subsequent optimization

## Workflow

```
Agent completes task
    ↓
Commissar receives output
    ↓
Commissar checklist:
  - Was research done? (data-backed?)
  - Are there obvious hallucinations?
  - Is token usage reasonable?
  - Does it deviate from the task objective?
    ↓
Pass → Forward downstream
Reject → Send back for rework + record reason
```

## Implementation Reference

The commissar is essentially an independent LLM call driven by a review prompt. It does NOT share the Agent's context window to avoid being "contaminated". Design guidelines:

- Use a separate System Prompt
- Have a clear review checklist
- Standardize output format (Pass/Reject + reason)

## Cost Control

Each commissar call adds to token consumption. Recommendations:

- Simple tasks: skip or 10% spot-check
- Medium-complexity tasks: 50% spot-check
- High-value / high-risk tasks: 100% review
