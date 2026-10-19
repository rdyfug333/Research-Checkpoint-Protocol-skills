---
name: research-checkpoint-protocol
description: Persist Scientific Experiment State across Research Checkpoints, Context Compaction Handoff, and Resume Across Sessions; preserve Frozen Decisions and safe Git Versioning. Use when initializing a research project, recording a verified milestone, handing work to another session, or resuming interrupted research.
---

# Research Checkpoint Protocol v1.0

Use this skill to keep durable research state in project files while discussion and execution remain in the conversation, Git records code history, and experiment logs and result files provide scientific evidence. Do not treat a summary or a Markdown status label as evidence.

Choose the requested mode: **Initialize**, **Checkpoint**, **Handoff**, or **Resume**. Read [references/protocol.md](references/protocol.md) for the procedure and use the matching templates in `assets/templates/` when creating project documents. Adapt templates to the project without inventing results, decisions, commits, or paths.

Keep the skill cross-project. Work only within the user's authorized project and requested scope. Preserve existing project instructions and research state. For Git synchronization, stage only reviewed files, exclude data and generated artifacts, never force push, and stop on unknown branch conflicts. A successful experiment and a successful Git sync are separate outcomes.

This protocol cannot intercept every automatic Context Compaction event. Use milestone checkpoints as the main safeguard, prepare a Handoff proactively when context is getting long (roughly 70–80% is a suggestion, not a fixed product threshold), and reread project files when resuming.
