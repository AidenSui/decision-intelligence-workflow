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

## Design Philosophy

This repository is a thinking scaffold, not a rigid execution script.

The workflow gives agents direction, vocabulary, schemas, and quality standards. It should help agents think more clearly, not force every decision through a mechanical checklist. Agents may combine, revisit, or compress layers when the situation calls for it, as long as they preserve the core contract:

- Keep the user's raw input.
- Find the upstream question.
- Separate constraints, assumptions, and emotional signals.
- Check whether continued testing, waiting, repair, or investment is still viable before recommending it.
- Expand the option set.
- Stress-test the advice.
- Give a falsifiable recommendation.

## Recommended Final Output Format

```markdown
## User Summary

- Recommendation type: test
- Recommendation: ...
- Core reason: ...
- Biggest risk or objection: ...
- First action: ...

## The Real Decision

...

## Options I See

...

## Key Judgment

...

## Strongest Objection

...

## Final Recommendation

...

## Next Steps

### 48 Hours

- ...

### 7 Days

- ...

### Later / Optional

- ...

## Stop Conditions

...
```

Internal layer labels should only be shown when the user explicitly asks for JSON, schema output, structured state, or workflow debugging.

## Recommendation-Type Specific Plans

Do not turn every recommendation into an experiment plan. Match the visible plan to the recommendation type:

- `commit`: use an execution plan.
- `test`: use a test plan.
- `delay`: use waiting conditions or an information plan.
- `reject`: use rejection rationale and alternative moves.
- `redesign`: use redesign direction and a new option structure.

Before using `test`, `delay`, repair, or continued investment, check whether the situation is still viable enough to deserve more time. More time is useful when it creates new evidence. It is harmful when it only extends a pattern that has already been repeatedly disproven.

The viability check is universal. It should consider:

- Disqualifiers: safety, legal, health, ethical, or severe downside issues.
- Prior attempts: whether the pattern has already cycled through hope, effort, promise, and relapse.
- Real desire vs avoidance: whether the user still wants the upside, or mainly fears the cost of leaving.
- Ownership: whether the person, team, market, institution, or system that must change shows real accountability.
- Non-negotiables: the minimum conditions required for continuing to be acceptable.
- Remaining value: what is still worth preserving, compounding, or repairing.

## Emotional Acknowledgement And Communication Scripts

If the decision clearly includes burnout, anxiety, identity pressure, relationship pressure, financial fear, or health risk, include 1-2 sentences acknowledging the emotional signal without letting it alone decide high-risk action.

If the decision materially affects a spouse, family member, cofounder, team, investor, manager, or another key stakeholder, include a short `Communication Script` of 5-8 natural sentences.

## Every Recommendation Must Be One Of Five Types

- `commit`: Do it directly.
- `test`: Run a low-cost experiment first.
- `delay`: Information is insufficient; wait for a specific trigger or signal.
- `reject`: Do not do it.
- `redesign`: The surface framing is too narrow; change the decision structure.

## Quality Standard

A good output must:

- Preserve the user's raw input without overwriting or sanitizing it.
- Translate casual language into structured decision state.
- Identify the more upstream question.
- Separate real constraints, emotional signals, and untested assumptions.
- Detect false binaries and hidden options.
- Produce a non-consensus view and explain what could make it wrong.
- Stress-test the recommendation with a contrarian challenge before finalizing it.
- Use an option stack when the real decision spans several domains and cannot be reduced to one clean choice.
- Do not recommend a test unless the thing being tested is still viable enough to deserve a test.
- Convert broad strategy into a staged test when the contrarian challenge exposes overload risk.
- Include a time-bounded decision gate for staged tests.
- Start final answers with a concise user summary.
- Avoid exposing internal layer labels by default.
- Prioritize next actions by time or order.
- Give an explicit recommendation instead of generic "it depends" advice.
- Detect whether later tactical questions are upstream decisions or downstream noise.
