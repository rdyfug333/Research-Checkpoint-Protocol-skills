# Research Project Instructions

> Template for a project that has no existing `AGENTS.md`. For an existing file, preserve its content and add only a clearly delimited RCP section.

## Project Goal and Scope

- Goal: [state the research question or project objective]
- Scope: [state included work and important boundaries]
- Current phase: [phase or `Needs Verification`]

## Working Principles

- Treat conversation as the place for discussion and execution, Markdown as durable state, Git as version history, and experiment logs/results as scientific evidence.
- Inspect the actual project and evidence before making claims about implementation or outcomes.
- Do not invent results, metrics, data provenance, commits, or decisions.
- Keep changes focused on the user's authorized project and task.

## Startup and Recovery

At the start of a new or resumed research task:

1. Read this file, `docs/PROJECT_STATE.md`, and `docs/DECISIONS.md`.
2. Read the latest `docs/SESSION_HANDOFF.md` if one exists.
3. Verify Git branch, HEAD, working tree, remote state, and relevant experiment configurations, logs, checkpoints, and outputs.
4. Compare recorded state with files and evidence; report conflicts or missing evidence before acting.
5. Continue only within the user's current authorization and from the last reliable checkpoint.

Use `$research-checkpoint-protocol` or natural language to request Initialize, Checkpoint, Handoff, or Resume. Read the installed Skill's `references/protocol.md` for the selected mode. The Skill cannot guarantee interception of automatic Context Compaction; save milestones and prepare handoffs proactively.

## Experiment Evidence and Status

Use `Planned`, `In Progress`, `PASS`, `PARTIAL`, `FAILED`, `BLOCKED`, or `Needs Verification`. A `PASS` requires evidence checked against acceptance criteria. Markdown claims and conversation summaries alone are not evidence. Record data version/split, configuration, random seed, code revision, metrics, and evidence paths when relevant.

## Frozen Decisions

Record important research decisions and their state in `docs/DECISIONS.md`. Do not silently change a Frozen decision because of a summary, compaction, or implementation convenience. Explain evidence and obtain the user's authorization before changing it unless already authorized.

## Git Safety

- Inspect status and diffs before staging; stage only reviewed paths needed for the milestone.
- Never use `git add .` for checkpoint commits. Exclude raw datasets, secrets, model weights, environments, and large caches.
- Commit and push only to an authorized repository and branch. Never force push, rewrite shared history, modify submodules, or resolve unknown conflicts automatically.
- Verify the remote SHA after push. Report experiment and Git synchronization outcomes separately.
- For important untracked experiment evidence, record its location, source, and backup information.

## Minimal Reproduction

Keep a concise, executable record of the code revision, data source/version and split, configuration, random seed, environment, and command needed to reproduce each important result. Preserve original evidence and identify any missing inputs; do not create extra tooling unless the project needs it.
