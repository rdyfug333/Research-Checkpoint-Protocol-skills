# Research Checkpoint Protocol (RCP)

Research Checkpoint Protocol v1.0 is a lightweight Codex Skill for preserving verifiable scientific experiment state across milestones, context compaction, and sessions. It does not run experiments or replace experiment evidence.

Long research projects can outlive a conversation or a computer session. RCP keeps the decisions, progress, and recovery entry point in files that can be inspected again.

RCP separates four responsibilities: conversation for discussion and execution, Markdown for durable state, Git for version history, and experiment logs/results for scientific evidence. The Skill itself is in [`.agents/skills/research-checkpoint-protocol/`](.agents/skills/research-checkpoint-protocol/), not at the repository root.

## Modes

| Mode | Purpose |
|---|---|
| Initialize | Create missing project state files and preserve existing `AGENTS.md` rules. |
| Checkpoint | Verify a meaningful milestone against real code, configuration, logs, metrics, and artifacts before recording its status. |
| Handoff | Write a short `docs/SESSION_HANDOFF.md` with the last reliable checkpoint and the next action. |
| Resume | Read durable state, verify Git and experiment files, then continue within the current authorization. |

## Repository layout

```text
.agents/skills/research-checkpoint-protocol/
├── SKILL.md
├── agents/openai.yaml
├── references/protocol.md
└── assets/templates/
    ├── AGENTS.md
    ├── PROJECT_STATE.md
    ├── DECISIONS.md
    └── SESSION_HANDOFF.md
VALIDATION_REPORT.md
LICENSE
CONTRIBUTING.md
RELEASE_NOTES.md
```

The first three templates are long-term project documents. `SESSION_HANDOFF.md` is generated only for a real Handoff and is a short-lived snapshot.

## Install on Windows

Run this in PowerShell from a directory where you want the checkout. Cloning a private copy requires repository access; a public copy can be cloned anonymously.

```powershell
git clone --branch v1.0.1 --depth 1 https://github.com/rdyfug333/Research-Checkpoint-Protocol-skills.git
if ($LASTEXITCODE -ne 0) { throw 'Git clone failed.' }
$source = Join-Path (Resolve-Path '.\Research-Checkpoint-Protocol-skills').Path '.agents\skills\research-checkpoint-protocol'
$skillsRoot = Join-Path $env:USERPROFILE '.agents\skills'
$target = Join-Path $skillsRoot 'research-checkpoint-protocol'
if (Test-Path -LiteralPath $target) { throw "Skill already exists: $target. Compare versions before replacing it." }
New-Item -ItemType Directory -Path $skillsRoot -Force | Out-Null
Copy-Item -LiteralPath $source -Destination $skillsRoot -Recurse
```

Alternatively, ask Codex to install the exact Skill subdirectory with its built-in Skill Installer:

```text
$skill-installer https://github.com/rdyfug333/Research-Checkpoint-Protocol-skills/tree/v1.0.1/.agents/skills/research-checkpoint-protocol
```

The built-in installer normally uses `$CODEX_HOME/skills` (typically `~/.codex/skills`); the PowerShell example uses the user-level `.agents/skills` location. Both are local Skill locations. If the Skill does not appear after installation, restart Codex.

## Quick start

In a Codex chat opened for the target research project, use one of these prompts:

```text
$research-checkpoint-protocol Initialize this project; preserve any existing AGENTS.md.
$research-checkpoint-protocol Checkpoint the completed milestone using the actual logs, metrics, and configuration.
$research-checkpoint-protocol Handoff the current task before changing sessions.
$research-checkpoint-protocol Resume from the last reliable checkpoint and report any conflicts first.
```

Initialize creates or supplements `AGENTS.md`, `docs/PROJECT_STATE.md`, and `docs/DECISIONS.md`. Checkpoint never treats a plan or summary as experimental `PASS`. Frozen Decisions require an explicit, evidence-backed change. Git synchronization stages reviewed paths only, excludes secrets/data/weights/caches, never force pushes, and verifies the remote SHA. Experiment status and Git sync status are separate.

RCP cannot intercept every automatic Context Compaction event. Milestone Checkpoints are the primary safeguard; a proactive Handoff near 70–80% context use is only a suggestion, not a fixed Codex threshold.

## Validation and license

[Validation report](VALIDATION_REPORT.md): Skill discovery, Initialize, Checkpoint, Handoff, conflict detection, and tested Git safety passed. Fresh-session Resume was **PARTIAL** because a third-party GICA submodule could not be fully inspected; one Frozen Decision safety check was also **PARTIAL** because it was non-blind. The report gives the evidence and remaining limits. No research data, model weights, or third-party source code are distributed here.

RCP source and documentation are licensed under the [MIT License](LICENSE), copyright (c) 2026 rdyfug333. Referenced third-party projects and resources keep their own licenses; this license does not claim ownership of them.

---

## 中文说明

RCP v1.0 是面向长期科研项目的 Codex Skill，用于在里程碑、上下文压缩和跨会话时保存可核验的研究状态。长期研究可能跨越多次对话或电脑环境，因此它把决策、进度和恢复入口写入可重新检查的文件。对话负责讨论与执行，Markdown 保存长期状态，Git 记录版本，实验日志和结果文件提供科学证据。Skill 本体位于 [`.agents/skills/research-checkpoint-protocol/`](.agents/skills/research-checkpoint-protocol/)。

四种模式：**Initialize** 非破坏性建立项目规则与状态；**Checkpoint** 核验真实证据后记录里程碑；**Handoff** 生成简短的当前任务快照；**Resume** 读取持久化文件并核对 Git 与实验文件后继续。`AGENTS.md`、`docs/PROJECT_STATE.md`、`docs/DECISIONS.md` 是长期文档，`docs/SESSION_HANDOFF.md` 仅用于交接。

上方 PowerShell 命令可安装固定版本 `v1.0.1`；也可在 Codex 中向 `$skill-installer` 提供上方的 GitHub Skill 子目录 URL。公开仓库可匿名克隆；私有仓库需要访问权限。安装后在科研项目对话中调用 `$research-checkpoint-protocol`，并明确提出 Initialize、Checkpoint、Handoff 或 Resume；上方 Quick start 给出了四个完整示例。例如：`$research-checkpoint-protocol Resume：先核对 Git、实验日志和最后可靠检查点，再报告冲突。`

实验 `PASS` 必须有可检查证据；Frozen Decisions 不会因新摘要而静默改变。Git 只提交审查过的文件，不提交数据集、密钥或权重，也不使用 Force Push。Skill 无法保证捕获每次自动 Context Compaction；约 70%–80% 的主动 Handoff 只是建议范围。

[验收报告](VALIDATION_REPORT.md)明确记录 Fresh-session Resume 和非盲测检查的 **PARTIAL** 限制。本仓库采用 [MIT License](LICENSE)，版权署名为 rdyfug333；提及的第三方项目及资源仍遵守各自许可证。
