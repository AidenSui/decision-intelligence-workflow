# Decision Intelligence Workflow

This is a reusable multi-layer decision workflow. It helps decide whether a decision is worth serious attention, what question should be asked instead, and how to produce clear, independent, non-consensus, falsifiable advice.

Core principle:

> One good decision saves one hundred downstream decisions.

This workflow does not automatically answer the user's surface question. It first asks: Is this an upstream decision? Is this question worth answering? Is there a more important question hiding underneath?

## File Structure

- `AGENTS.md`: Start instructions for coding agents or AI assistants using this repository.
- `prompts/orchestrator.md`: Main orchestrator prompt for state management, routing, follow-up questions, synthesis, and anti-noise control.
- `prompts/agents.md`: Formal prompt library for each layer agent, including the contrarian challenge agent.
- `schemas/decision_workflow.schema.json`: Complete JSON schema for structured inputs and outputs.
- `workflow.yaml`: Workflow order, layer inputs and outputs, and gate conditions.
- `templates/state_template.json`: State template for each new decision session.
- `examples/sample_run.json`: A complete example from raw input to recommendation.

## Quick Start After Pulling This Repo

After cloning or pulling this repository, a user can ask an agent:

```text
Read AGENTS.md and use the Decision Intelligence Workflow in this repo.

Decision:
...

Background:
...

Current options:
...

Start with Layer 1 and Layer 2 only. Do not give a final recommendation yet.
```

The agent should then read `AGENTS.md`, load the orchestrator and agent prompts, and begin the workflow from the current repository contents.

## Recommended Usage

1. Read `AGENTS.md` first if you are an AI agent operating inside this repository.
2. Use `prompts/orchestrator.md` as the main agent system prompt.
3. Use `prompts/agents.md` as the prompt library for sub-agents or tool agents.
4. For every new decision request, run the Layer 1 parser first.
5. If material information is missing, run the Layer 2 deep dive question agent before giving advice.
6. After the user answers, store the raw answers in Layer 3.
7. Then run Layers 4-7 to produce the reframe, option set, evaluation, and non-consensus insight.
8. Run Layer 8 to challenge the emerging recommendation from a skeptical, practical, adversarial point of view.
9. Run Layer 9 to produce the final recommendation, which must answer the strongest contrarian objection.
10. For later tactical questions, run the Layer 10 anti-noise guardrail first.

## Recommended Final Output Format

```markdown
## 1. Restate The Problem

Raw input:
> ...

My understanding:
...

## 2. The Surface Question

...

## 3. The Better Question

...

## 4. Does This Decision Matter?

Conclusion:
...

Reason:
...

## 5. Follow-Up Questions

1. ...
2. ...
3. ...

## 6. Option Set

A. ...
B. ...
C. ...
D. Hidden option: ...

## 7. Non-Consensus View

Most people would probably say:
...

I do not fully agree because:
...

The real variable I care about:
...

## 8. Recommendation

I recommend:
...

Confidence:
...

Reason:
...

Strongest objection:
...

Why the recommendation still survives, or how it changed:
...

## 9. Next Actions

1. ...
2. ...
3. ...

## 10. Kill Or Reversal Criteria

This recommendation should be overturned if:
...
```

## Every Recommendation Must Be One Of Five Types

- `commit`: Do it directly.
- `test`: Run a low-cost experiment first.
- `delay`: Information is insufficient; wait for a specific trigger or signal.
- `reject`: Do not do it.
- `redesign`: The user's question is wrong; change the decision structure.

## Quality Standard

A good output must:

- Preserve the user's raw input without overwriting or sanitizing it.
- Translate casual language into structured decision state.
- Identify the more upstream question.
- Separate real constraints, emotional signals, and untested assumptions.
- Detect false binaries and hidden options.
- Produce a non-consensus view and explain what could make it wrong.
- Stress-test the recommendation with a contrarian challenge before finalizing it.
- Give an explicit recommendation instead of generic "it depends" advice.
- Detect whether later tactical questions are upstream decisions or downstream noise.
