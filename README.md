# Research Checkpoint Protocol v1.0

Research Checkpoint Protocol（RCP）帮助长期科研项目在上下文压缩、对话中断和环境切换后恢复可信状态。核心分工是：对话用于讨论与执行，Markdown 保存长期状态，Git 记录版本，实验日志和结果文件提供科学证据。

## 四种模式

- **Initialize**：检查项目已有规则和状态；缺少时创建核心文档，已有内容则保留并非破坏性补充。
- **Checkpoint**：核验代码、数据划分、配置、日志、Checkpoint 和指标后，记录一个有效研究里程碑。
- **Handoff**：生成精简的 `docs/SESSION_HANDOFF.md`，记下当前任务、可靠检查点和准确下一步。
- **Resume**：按恢复顺序读取状态文档，核对 Git 和实验文件，再从最后一个可靠检查点继续。

## 状态文档

`AGENTS.md` 保存低频项目规则和完整恢复流程；`docs/PROJECT_STATE.md` 保存当前阶段、实验状态、结果和下一步；`docs/DECISIONS.md` 保存重要决策及其历史。`docs/SESSION_HANDOFF.md` 是短期恢复快照，不能替代前三份长期记录。

状态使用 `Planned`、`In Progress`、`PASS`、`PARTIAL`、`FAILED`、`BLOCKED` 或 `Needs Verification`。缺少可检查证据时，不得写 `PASS`。

## 安装

将仓库内 `.agents/skills/research-checkpoint-protocol` 目录复制到用户级 `.agents/skills/`，保持目录名 `research-checkpoint-protocol`。Codex 通常从用户级 `.agents/skills` 和项目级 `.agents/skills` 发现 Skills。也可在项目中直接使用本仓库提供的 Skill 源码。更新时从本仓库维护版本重新复制；不要在多个科研项目中维护副本。

显式调用：`$research-checkpoint-protocol`。也可以用自然语言提出 Initialize、Checkpoint、Handoff 或 Resume。

## 常见流程

新项目初始化：在目标科研项目中调用 Skill 并请求 Initialize。它先检查现有 `AGENTS.md`、文档和 Git 状态，再创建缺少的状态文件；不会覆盖已有 `AGENTS.md`，也不会为模板填入虚构结果。

完成关键实验后请求 Checkpoint，并给出验收标准。Skill 会核对真实日志、配置、代码版本和结果文件；证据不足时记录 `Needs Verification` 等状态。正式验收通过后，只有目标仓库和分支已授权且拟提交文件经过检查，才进行 Git Commit + Push。

开始新对话或恢复中断工作时请求 Resume。Skill 先读取规则、项目状态、决策和最新 Handoff（如存在），再核验分支、HEAD、工作区、远程状态和所需实验文件。

## Git 同步安全

只暂存审查过的必要源码、配置和 Markdown；排除原始数据集、密钥、模型权重、虚拟环境和大型缓存。不使用 `git add .` 或 Force Push，不自动解决未知分支冲突或修改 Submodule。Push 后核对远程 Commit SHA。实验 `PASS` 与 `Git Sync: FAILED` 可以同时成立。

## Context Compaction 边界

Skill 规范保存和恢复动作，无法仅凭 `SKILL.md` 拦截所有自动 Context Compaction。里程碑 Checkpoint 是主要保障；在上下文使用率约 70%–80% 时主动 Handoff 只是建议范围，不是所有 Codex 版本的固定阈值。

## 后续阶段

Phase 2 将在用户指定的真实科研项目（PSS-Reproduction）部署并核验状态协议。Phase 3 将单独进行跨对话恢复验收；本仓库 v1.0 交付不启动这两个阶段。
