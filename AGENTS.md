# Agent Start Instructions

This repository is a prompt-and-schema package for running the Decision Intelligence Workflow.

If a user asks you to "use this repo", "run this workflow", "help me make a decision", or "start the decision intelligence workflow", follow these instructions.

## What This Repo Contains

- `prompts/orchestrator.md`: The primary operating prompt. Read this first.
- `prompts/agents.md`: The specialized layer prompts. Use this as the agent library.
- `workflow.yaml`: The execution order and gate logic.
- `schemas/decision_workflow.schema.json`: The structured output schema.
- `templates/state_template.json`: The starting state shape for a new decision session.
- `examples/sample_run.json`: A reference example for expected output quality.

## How To Start

1. Read `prompts/orchestrator.md`.
2. Read `prompts/agents.md`.
3. Use `workflow.yaml` to follow the layer order.
4. Use `schemas/decision_workflow.schema.json` as the output contract.
5. Start with Layer 1 unless the user explicitly asks for a later layer.

## Default Behavior

When the user provides a decision request:

1. Preserve the raw user input exactly.
2. Run Layer 1: Raw Input Parser.
3. If material information is missing, run Layer 2 and ask no more than 7 deep-dive questions.
4. Wait for the user's answers.
5. After answers arrive, run Layers 3-10.
6. The final recommendation must consume and answer the Layer 8 contrarian challenge.

## How To Use The Materials

Treat this repository as a thinking scaffold, not a rigid script.

The prompts, schema, workflow, and example record provide direction, vocabulary, and quality standards. They should open the agent's thinking rather than force a mechanical sequence. If the user's situation clearly calls for combining layers, revisiting an earlier layer, or skipping an unnecessary intermediate step, do that and explain the reason briefly.

The output contracts matter more than the internal workstyle. Preserve raw input, surface the upstream question, identify constraints and hidden options, stress-test the advice, and produce a falsifiable recommendation. Do not complete checklist items merely because they exist.

## User-Facing Starter Prompt

The user can start the workflow with:

```text
Use the Decision Intelligence Workflow in this repo.

Decision:
...

Background:
...

Current options:
...

Start with Layer 1 and Layer 2 only. Do not give a final recommendation yet.
```

After the user answers the deep-dive questions, continue with:

```text
Continue from my answers. Run Layers 3-10 and give the final recommendation.
Make sure the final recommendation responds to the contrarian challenge.
```

## Important Rules

- Do not answer the user's surface question immediately.
- First decide whether the surface question is upstream, downstream, or a proxy for another issue.
- Do not optimize a bad question.
- Detect false binaries and hidden options.
- Use an option stack when a single-option answer would hide the real structure of the decision.
- If the contrarian challenge shows overload risk, convert a broad plan into a staged test with a decision gate.
- Make recommendations falsifiable.
- Every final recommendation must be one of: `commit`, `test`, `delay`, `reject`, or `redesign`.
- If the user later asks a tactical question, run Layer 10: Anti-Noise Guardrail first.

## If The User Wants An Output File

If the user asks you to save the result, create a decision record under a local `work/` directory using this pattern:

```text
work/decision-record-YYYY-MM-DD.md
```

The `work/` directory is intended for private local decision records and should not be treated as part of the reusable workflow package.
