# CodexHost Workflow

面向 CodexHost 的质量优先协作技能：**Codex 策划与分包验收，DeepSeek Harness（DSH）作为唯一执行调度者。**

适用于希望使用多个执行成员、控制主控上下文、处理 Codex 额度中断，同时保留明确验收标准的个人项目。

## 分工与约束

- Codex 负责版本化计划、关键技术决策、分包审查及必要的集成验收。
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

在 CodexHost 中打开目标业务项目，先在 Codex 会话中调用：

```text
使用 $codexhost-workflow，角色 planner。
项目路径：【填写绝对路径】
目标：【填写本次功能或问题】
先核对项目规则和现有改动，形成版本化计划，明确验收标准、回退点和停止条件。
```

审阅并批准计划后，在同项目的 DSH 会话中加载 `codexhost-workflow`，指定 `dispatcher` 角色及获批计划。DSH 网页也可用 `/codexhost-workflow` 显式调用。

交付后，在 Codex 指定 `reviewer` 角色，提供原计划、包ID/修订和证据入口，审查实际成果。

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
| [references/artifacts.md](references/artifacts.md) | 计划、状态、brief、回执和验收记录的字段示例 |
| [TRYOUT.md](TRYOUT.md) | 试用入口与试用后的反馈材料 |

## 验证范围

首版已做技能格式检查、Codex/DSH 原生技能发现与读取检查，以及独立的文档一致性和压力场景评估。

这些检查不代表真实业务验收。项目质量、团队实际行为、成员模型选择、重启恢复和额度节省，仍需在具体项目中验证。

本技能是行为指南，不是后台调度服务、权限沙箱或计费硬限；不会自动检测额度、创建接管窗口或转移原生 Team 所有权。
