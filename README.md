# CodexHost Workflow

面向 CodexHost 的质量优先协作技能：**你告诉 Codex 目标，Codex 衔接计划、DSH 调度与成果验收。** DeepSeek Harness（DSH）是唯一执行调度者。

适用于希望使用多个执行成员、控制主控上下文、处理 Codex 额度中断，同时保留明确验收标准的个人项目。

## 分工与约束

- Codex 主控负责计划、建立或复用 DSH 调度会话、跟进交付、关键技术决策、分包审查及必要的集成验收。
- DSH 按获批计划形成 brief、安排成员、组织自测和普通修复；执行完成先进入待验收。
- 授权计划、当前状态和重要决策分别维护，不允许执行者自行降低验收标准。
- 有修改的任务开始前建立覆盖已有未提交改动的回退点。
- 按任务点名必要技能，确认实际可见和已加载。
- 新 Codex 窗口可以继续审查；新 DSH 会话不自动接管旧 Lead 的原生团队。

## 安装

仓库根目录就是技能目录。将它克隆到共享技能根 `~/.agents/skills/codexhost-workflow`，可供支持该目录的 Codex 与 DSH 发现。

Windows PowerShell：

```powershell
$skillRoot = Join-Path $env:USERPROFILE '.agents/skills'
New-Item -ItemType Directory -Path $skillRoot -Force | Out-Null
git clone https://github.com/Nniuniu-nn/codexhost-workflow.git (Join-Path $skillRoot 'codexhost-workflow')
```

macOS / Linux：

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/Nniuniu-nn/codexhost-workflow.git ~/.agents/skills/codexhost-workflow
```

如果目标目录已有技能、联接或其他内容，先核对其来源，不要覆盖。此仓库不会安装 CodexHost、DSH 或自动修改业务项目。

## 开始使用

在 CodexHost 中打开目标业务项目，在 Codex 会话里说：

```text
使用 $codexhost-workflow 完成这个任务：修复面试记录页刷新后记录消失的问题。
由你安排 DSH 调度、跟进交付并验收，需要我决定的事情再问我。
```

把示例目标换成自己的需求即可。默认进入 Codex 主控模式；计划、任务编号、依赖、DSH 会话绑定和验收材料由它们整理，不需要你填写。项目不明确时才询问路径。

你继续在这个 Codex 会话沟通。它应实际调用 CodexHost 创建或复用 DSH 调度会话，跟进交付，收到成果后审查代码与证据；需补正时交回原 DSH，由它安排修复。DSH 自测不能代替 Codex 验收。

若只想讨论，可明确说“先讨论，不执行”。`planner`、`dispatcher`、`reviewer` 是内部职责或高级单独入口，不是每次使用时必须手动切换的三个步骤。

完整提示词和试用步骤见 [TRYOUT.md](TRYOUT.md)。

## 需要另外准备的能力

- 可用的 CodexHost 和 DSH 运行环境。
- 若使用原生 Agent Teams，需要在相应 DSH profile 中明确启用，并核对当前版本支持情况。
- 调试、非平凡逻辑修改和完成声明分别使用 `systematic-debugging`、`test-driven-development`、`verification-before-completion` 等相关技能；网页交互按需使用 `agent-browser`。
- 辅助技能不随本仓库分发。先安装并确认会话目录可见；缺失时按规则报告，不假装已加载。

## 文件

| 文件 | 用途 |
|---|---|
| [SKILL.md](SKILL.md) | 角色、质量门、交接与额度中断规则 |
| [references/orchestration.md](references/orchestration.md) | Codex 主控的原生会话衔接与交付跟进 |
| [references/artifacts.md](references/artifacts.md) | 计划、状态、brief、回执和验收记录的字段示例 |
| [TRYOUT.md](TRYOUT.md) | 试用入口与试用后的反馈材料 |

## 验证范围

首版已做技能格式检查、Codex/DSH 原生技能发现与读取检查，以及文档和压力场景评估。试用反馈后，默认入口已改为 Codex 主控，取消用户手动搬运计划、任务编号和回执的步骤。
此次入口修订做了格式、引用检查与独立的只读场景评估；没有据此宣称真实的自动派发至验收闭环已通过业务试用。

这些检查不代表真实业务验收。项目质量、团队实际行为、成员模型选择、重启恢复和额度节省，仍需在具体项目中验证。

本技能是行为指南，不是后台调度服务、权限沙箱或计费硬限；不会自动检测额度、创建接管窗口或转移原生 Team 所有权。
