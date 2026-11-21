---
title: agent-skill
author: Jerry.Baijy
tags:
  - dev
  - ai
  - agent
  - skill
---

# Overview

[**Agent Skill**](https://agentskills.io/) 是一种轻量级、开放的格式，用于以专业知识和工作流程为 [AI Agent](ai-agent.md) 扩展能力。

Agent Skill 最初由 Anthropic 开发，用于 Claude Platform，现作为开放标准。

> [Agent Skills - Anthropic 开放规范](https://agentskills.io/)
>
> [Agent Skills - Claude Platform Docs](https://platform.claude.com/docs/zh-CN/agents-and-tools/agent-skills/overview)
>
> [Anthropic Skills - GitHub](https://github.com/anthropics/skills)：示例技能
>
> [WorkBuddy 开放文档](https://open.workbuddy.cn/docs/skill#技能基础结构)

# 目录结构

一个 skill 的目录包含 `SKILL.md` 和[**可选目录**](https://agentskills.io/specification#optional-directories)组成。

```markdown
my-skill/
    ├── SKILL.md              # 技能定义（必须）
    ├── references/           # 参考资料（可选）
    │   ├── api-spec.md       # API 规范、字段类型等
    │   └── examples.md       # 示例数据
    ├── scripts/              # 可执行脚本（可选）
    │   ├── fetch-data.js     # 数据获取脚本
    │   └── transform.py      # 数据处理脚本
    ├── templates/            # 模板文件（可选）
    │   ├── report.sh         # 报告生成模板
    │   └── workflow.sh       # 工作流模板格式
    └── ...
```

# `SKILL.md`

[`SKILL.md`](https://agentskills.io/specification#skill-md-format) 由 **YAML Front Matter** 和 **Body Content** 两部分组成。

Agent 执行技能时会**完整读取 `SKILL.md` 作为上下文。

## 最简示例

```markdown
---
name: your-skill-name
description: 一句话描述技能能力
version: 1.0.0
---
 
# 技能指令正文
 
当用户需要做 XX 时，按以下步骤执行：
1. ...
2. ...
3. ...
```

## YAML Front Matter

> [!CAUTION]
>
> 此处的 [YAML Front Matter](<yaml.md#YAML Front Matter>) 字段是 [WorkBuddy 开放文档](https://open.workbuddy.cn/docs/skill#技能基础结构)的要求。

| **字段**        | **必填** | **说明**                                             |
| :-------------- | :------- | :--------------------------------------------------- |
| name            | 是       | 技能标识                                             |
| display_name    | 是       | 技能在市场上的中文展示名称                           |
| display_name_en | 是       | 技能在市场上的英文展示名称                           |
| description     | 是       | 写清用途和触发词                                     |
| description_zh  | 是       | 简短中文介绍，在市场上展示在技能详情页               |
| description_en  | 是       | 简短英文介绍，在市场上展示在技能详情页               |
| allowed-tools   | 否       | 工具白名单（逗号分隔）                               |
| version         | 是       | 版本号                                               |
| examples_zh     | 否       | skill 使用案例（中文版），展示在详情页【试试这样用】 |
| examples_en     | 否       | skill 使用案例（英文版），展示在详情页【试试这样用】 |
| author          | 是       | 合作方名称                                           |

## Body Content

[**Body Content**](https://agentskills.io/specification#body-content) 包含技能指令。没有格式限制。写任何帮助代理人有效完成任务的内容。

## 其它说明

Anthropic 建议，保持 `SKILL.md` 在 500 行以下，将详细参考资料转移到[可选目录](https://agentskills.io/specification#optional-directories)中。

# `references`

[`references`](https://agentskills.io/specification#references/) 是 skill 的[可选目录](https://agentskills.io/specification#optional-directories)，用于存放 `SKILL.md` 引用的补充知识文档，Agent 执行技能时会**按需读取**这些文件作为上下文。

适用场景：API 字段类型定义、协议规范、领域知识参考、示例数据等。

```
references/
├── field-types.md           # 字段类型枚举和用法
├── api-endpoints.md         # API 接口文档
└── best-practices.md        # 最佳实践指南
```

## 使用方式

### Anthropic

```markdown
See [the reference guide](references/REFERENCE.md) for details.

Run the extraction script:
scripts/extract.py
```

### WorkBuddy

在 `SKILL.md` 中通过 `@references/xxx.md` 引用。

# `scripts`

[`scripts`](https://agentskills.io/specification#scripts/) 是 skill 的[可选目录](https://agentskills.io/specification#optional-directories)，用于存放技能执行中需要调用的脚本，Agent 执行技能时会**按需读取**这些文件作为上下文。

适用场景：调用外部 API、数据处理、批量操作、需要特定运行时的逻辑。

使用方式：在 `SKILL.md` 中声明调用命令和参数。

示例：

```markdown
scripts/
├── data-index.js            # 数据查询入口
└── tool-index.js            # 工具集入口
```

# `templates`

`templates` 用于存放可复用的模板脚本或配置文件。

适用场景：标准化操作流程的模板、报告生成模板。

示例：

```mark
templates/
├── authenticated-session.sh  # 认证会话模板
└── capture-workflow.sh       # 数据采集工作流模板
```

# 渐进披露

Agent 逐步加载技能， 只有在任务需要时才会调入更多细节。

- Agent 首先读取 `SKILL.md` 中的 YAML Front Matter，仅仅知道该技能何时可能相关。
- 当你问到具体事情时，Agent 会把你的问题和 YAML Front Matter 对应起来，并把 `SKILL.md` 的 Body Content 加载到上下文中。
- 只有在需要时才会加载 `references` 和 `scripts` 等[可选目录](https://agentskills.io/specification#optional-directories)中的其它细节文件。
- 最后通过读取到的指令，完成用户的请求。

# 相关条目

- [`skills-ref`](https://github.com/agentskills/agentskills/tree/main/skills-ref)：验证 skill 是否符合 Anthropic 规范
