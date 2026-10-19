# Research Checkpoint Protocol v1.0.1 — Public Release

Draft release notes for the `v1.0.1` tag. Publishing the tag alone does not create a GitHub Release or change repository visibility.

Compared with `v1.0`, this release adds public documentation, a confirmed MIT license, contribution guidance, and a release draft. The validated Skill workflow is unchanged.

## What is RCP?

RCP is a lightweight Codex Skill that preserves evidence-backed scientific project state across research milestones, context compaction, and sessions. It keeps project rules, current state, decisions, and short handoffs in Markdown while verifying claims against source, Git, and experiment artifacts.

## Core modes

- **Initialize:** create missing durable project documents without overwriting existing `AGENTS.md` rules.
- **Checkpoint:** record a meaningful, verified research milestone.
- **Handoff:** save a concise recovery snapshot for the next session.
- **Resume:** reconcile durable documents with actual Git and experiment state before continuing.

## Installation and requirements

See the [README](README.md#install-on-windows) for a PowerShell installation pinned to `v1.0.1` and the Codex Skill Installer prompt targeting the Skill subdirectory. Codex must support local Skills from `.agents/skills` or `$CODEX_HOME/skills`. The Skill consists of Markdown, YAML metadata, and templates; it has no runtime package dependencies.

## Validation summary

The official Skill Creator validator passed. Initialize, Checkpoint, Handoff, conflict detection, and tested Git safety passed. Fresh-session Resume remains **PARTIAL** because full inspection of a third-party GICA submodule worktree was permission limited. A Frozen Decision refusal check was **PARTIAL** because it was performed in the same session without blinding. See [VALIDATION_REPORT.md](VALIDATION_REPORT.md) for the evidence and full scope.

## Known limitations

- RCP cannot guarantee interception of automatic Context Compaction; it relies on milestone Checkpoints and proactive Handoffs.
- A Markdown status label alone does not prove an experiment passed. Users must retain and verify source, configuration, data references, logs, metrics, and artifacts.
- The repository does not distribute research datasets, model weights, or third-party source code.
- Git synchronization requires an authorized repository and branch. Push success requires a matching remote SHA.

License: [MIT](LICENSE), copyright (c) 2026 rdyfug333.
