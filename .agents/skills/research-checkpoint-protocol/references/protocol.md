# Research Checkpoint Protocol v1.0

## Operating model

Four sources have different jobs: conversation supports discussion and execution; Markdown preserves durable research state; Git records versioned changes; experiment logs, configurations, checkpoints, and result files provide scientific evidence. None replaces the others. A written `PASS` is a claim to verify, not proof.

Use only the mode requested or clearly implied by the user. Resume does not authorize every listed follow-up task. Do not create a checkpoint for routine reading, explanation, or a small edit; checkpoint meaningful completed milestones.

## Shared evidence and status rules

Use `Planned`, `In Progress`, `PASS`, `PARTIAL`, `FAILED`, `BLOCKED`, or `Needs Verification` as appropriate. `PASS` requires inspectable evidence of the acceptance criteria. If evidence is absent, contradictory, stale, or inaccessible, use `Needs Verification` or another supported status and explain why. Do not infer experiment outcomes from plans, summaries, intended configurations, or conversation alone.

When relevant, record code revision, data source/version and split, configuration, random seed, run command/environment, metrics, checkpoint identity, and evidence paths. Identify evidence that is external to Git and preserve its location and backup information. Compute SHA-256 for important files when it aids identity or integrity checks.

Frozen Decisions are not silently changed because of compaction, a new summary, or an implementation convenience. Explain the evidence and ask the user before changing a frozen scientific decision unless the user already authorized that exact change.

## Mode A — Initialize

1. Inspect the project root, current instructions, Git state, and existing `AGENTS.md`, `docs/PROJECT_STATE.md`, and `docs/DECISIONS.md`.
2. If a file exists, read it and preserve its content. Never replace an existing `AGENTS.md`. Add only a clearly delimited RCP section when needed, or leave it intact and report an incompatible instruction conflict.
3. If a core file is missing, create it from the corresponding template, adapting headings and removing irrelevant prompts without fabricating project facts.
4. Do not create `SESSION_HANDOFF.md` during routine initialization. Do not initialize unrelated projects or generate unrelated documentation.
5. Report created, supplemented, and unchanged files and any facts that still need verification.

## Mode B — Checkpoint

1. Read project rules and current state, then inspect the actual code, data split, run configuration, logs, checkpoint files, and metrics relevant to the milestone.
2. Compare evidence against explicit acceptance criteria. Record `PASS`, `PARTIAL`, `FAILED`, `BLOCKED`, or `Needs Verification` with a concise basis; separate experimental outcome from Git sync outcome.
3. Update `PROJECT_STATE.md` with the milestone, evidence paths, revision, data/config/seed and metrics where applicable. Update `DECISIONS.md` only when an important research decision changes, preserving its history and state.
4. Before a Git commit, inspect the diff and explicitly identify intended files. Stage only necessary source, configuration, and Markdown. Exclude raw datasets, secrets, model weights, environments, large caches, and unrelated modifications. Do not use `git add .`.
5. Commit and push only when the repository and target branch are authorized and the user has authorized sync (an explicit standing authorization in the task counts). Never force push, modify submodules, resolve unknown branch conflicts, or claim a push succeeded without checking the remote SHA.
6. If experiment evidence passes but synchronization fails, record `Experiment: PASS` and `Git Sync: FAILED`, with the error and recovery step.

## Mode C — Handoff

1. Read the three core documents and inspect current Git and relevant experiment state.
2. Create or refresh `docs/SESSION_HANDOFF.md` using the template. State the active task, last reliable checkpoint, completed and remaining work, key frozen decisions, source/evidence paths, branch/HEAD/working tree/push status, precise next action, and questions requiring the user.
3. Keep this as a concise short-term snapshot. Do not paste chat history or duplicate the full state and decision records. A normal handoff is local and does not require a commit or push.
4. Make uncertainty and missing evidence explicit. Do not elevate an unverified result to a reliable checkpoint.

## Mode D — Resume

1. Read `AGENTS.md`, `docs/PROJECT_STATE.md`, and `docs/DECISIONS.md`, in that order; then read the latest `docs/SESSION_HANDOFF.md` if present.
2. Verify branch, HEAD, tracked and untracked changes, and remote status. Inspect experiment configs, logs, checkpoints, outputs, and data references needed for the proposed continuation.
3. Compare the handoff with durable state and actual files. Report stale snapshots, missing checkpoints, contradictory records, and Git inconsistencies before proceeding.
4. Continue from the last reliable checkpoint only within the user's current authorization. Do not automatically rerun training or change Frozen Decisions to resolve a discrepancy. Ask for direction when the discrepancy blocks safe continuation.

## Non-destructive project instructions

When adding RCP guidance to an existing `AGENTS.md`, retain all existing text and place additions under an explicit heading such as `## Research Checkpoint Protocol`. Do not edit or delete unrelated instructions. If project rules conflict, follow higher-priority instructions and describe the conflict rather than overwriting either side.

## Context Compaction boundary

This skill defines save and recovery practices; it does not register a background listener, modify Codex compaction internals, or guarantee interception of automatic compaction. Milestone checkpoints are primary. A proactive handoff around 70–80% context use is an optional reminder range, not an official fixed threshold for every Codex version.

## Git safety and evidence

- Confirm the authorized repository and branch before synchronization; inspect `git status`, diff, and staged diff.
- Stage paths explicitly. Exclude raw data, credentials, weights, virtual environments, and large generated caches. Keep locations and backup details for important untracked evidence in state documents.
- Do not force push, rewrite shared history, modify submodules, or resolve unknown branch divergence automatically.
- Verify the remote branch SHA after push. Report authentication or repository discovery failures without speculative URL changes or risky credential reconfiguration.
- Classify Git sync failures from the observed command and error: sandbox/filesystem permission denial, DNS or network failure, authentication/authorization failure, or remote history divergence. Record the actual error and leave Git Sync as FAILED or BLOCKED until resolved. Do not infer repository absence from a private-repository 404 alone. Only a successful push followed by a matching remote branch SHA is Push Success.
- A Git commit records files, not scientific validity. A scientific `PASS` records evidence, not remote synchronization.
