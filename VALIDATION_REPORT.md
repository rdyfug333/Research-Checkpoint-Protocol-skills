# Research Checkpoint Protocol v1.0 — Final Validation

This report records v1.0 validation and the repository state at the time it was written. See `RELEASE_NOTES.md` for the later public packaging update.

Date: 2026-10-19 (Asia/Shanghai)

## Objective and functions

RCP preserves evidence-backed scientific state across milestones, compaction, and sessions using Markdown and Git. It provides **Initialize**, **Checkpoint**, **Handoff**, and **Resume**. Experiment evidence remains in source, configurations, logs, CSVs, checkpoints, and outputs; a status label alone is not proof.

## Acceptance record

| Stage | Result | Basis |
|---|---|---|
| Phase 0 protocol design | PASS | Four modes and evidence/Git/Frozen Decision boundaries are defined in the installed `SKILL.md` and `references/protocol.md`. |
| Phase 1 build and installation | PASS | Skill source at commit `40a0422`; seven installed skill files were byte-identical to source before the final wording fix. Skill Creator `quick_validate.py` passed for source and installation with UTF-8 mode. |
| Phase 2 PSS deployment | PASS for RCP deployment; PSS research remains PARTIAL | PSS `AGENTS.md`, `docs/PROJECT_STATE.md`, `docs/DECISIONS.md`, and `docs/SESSION_HANDOFF.md` exist at PSS HEAD `fcfb386`. State cites Phase 0–3 implementation and local experiment evidence, with strict paper reproduction explicitly PARTIAL. |
| Phase 3 Test A | PARTIAL | Fresh-session Resume recovered the main research state, frozen choices, metrics and next task. Full GICA submodule worktree inspection was Permission Limited. Evidence: Codex chat “RCP Phase 3”, final Test A report. |
| Phase 3 Test B | PASS | Independent blind Resume found B1 metric conflict, B2 Frozen Decision/source conflict, and B3 stale Handoff without altering originals. Evidence: PSS `.rcp_test_b/TEST_B_REPORT.md`, fixture commits `9026737` and `0986b5a`. |
| Phase 3 Test C | C1 PASS; C2 PASS; C3 PASS; C4 PARTIAL | Safe commit `a7378ca`, verified local bare push, divergence stopped with local `0441661` and remote `7af47d8`. C4 was a non-blind same-session safety check, supported by independent Test B evidence. Evidence: PSS `.rcp_test_c/TEST_C_REPORT.md` and local fixture Git repositories. |

| Capability | Result | Evidence boundary |
|---|---|---|
| Skill Discovery | PASS | Test A loaded installed Skill. |
| Initialize | PASS | Phase 2 created durable PSS state without changing research algorithms. |
| Checkpoint | PASS | Phase 2 recorded inspectable research evidence and separate status. |
| Handoff | PASS | Phase 2 produced a recoverable index; Test A recognized its later stale task line. |
| Fresh-Session Resume | PARTIAL | Main state restored; GICA recursive Git status remained Permission Limited. |
| Evidence Verification | PASS | Tests A/B checked source and CSV values; this is targeted, not an audit of every PSS artifact. |
| Conflict Detection | PASS | Test B independently detected B1–B3. |
| Frozen Decision Protection | PASS | Test B independent detection; Test C4 same-session non-blind refusal. |
| Git Safe Commit | PASS | Test C1 staged and committed only five reviewed fixture files. |
| Git Push Verification | PASS | Test C2 matched local and bare-remote SHA. |
| Failure Handling | PASS for tested divergence; PARTIAL coverage overall | Test C3 stopped on `1 1` divergence. Permission, DNS/network, authentication, and private-repository 404 are classified in the final protocol wording but were not all induced dynamically. |

## Corrections and limits

Test C found one narrow documentation gap: the Git guidance did not explicitly distinguish sandbox permission denial, DNS/network failure, authentication failure, and divergence. A single Git-safety line was added to `references/protocol.md`. No new feature or research-method change was made.

RCP's Markdown/Git persistence does **not** guarantee automatic capture of every Context Compaction event. PSS GICA submodule metadata has a third-party permission restriction, so full recursive status remains unverified. PSS datasets, weights and experiment CSVs are local-only and were not published with this Skill. A private repository may return 404 to an unauthorized connector; Git remote synchronization is the release authority.

User-level installation: `$HOME/.agents/skills/research-checkpoint-protocol`. Repository source: `.agents/skills/research-checkpoint-protocol`.

## Release record

Target private repository: `https://github.com/rdyfug333/Research-Checkpoint-Protocol-skills.git`; authorized branch: `main`. Before this report was committed, Git HTTPS verified remote `main` at `40a0422d7cdff89abdd89a9223f932a372111a7e` and found no remote `v1.0` tag. At report preparation, publication status is **RCP v1.0 — VALIDATED, RELEASE PENDING**. After publication, the authoritative release record is the remote `main` SHA plus the peeled annotated `v1.0` tag SHA; both must match the release commit. This report records the pre-publication gate without predicting a future push or tag.
