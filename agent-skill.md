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

[**Skill**](https://agentskills.io/) 是一种为 [Agent](ai-agent.md) 提供新能力的标准化的方式。

> [WorkBuddy 开放文档](https://open.workbuddy.cn/docs/skill#技能基础结构)

# 目录结构

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

[SKILL.md](http://skill.md/) 使用 YAML frontmatter + Markdown 正文： 

```markdown
---
name: your-skill-name
display_name: 展示名称
display_name_en:切英文版展示名称
description: 一句话描述技能能力
description_zh: 简短中文介绍
description_en: A Brief English Introduction
examples_zh:
- "案例 1"
- "案例 2"
- "案例 3"
examples_en:
- "example 1"
- "exmaple 2"
- "example 3"
version: 1.0.0
author: "合作方名称"
---
 
# 技能指令正文
 
当用户需要做 XX 时，按以下步骤执行：
1. ...
2. ...
3. ...
```

**Frontmatter 字段**：

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

# `references`

`references` 用于存放 `SKILL.md` 引用的补充知识文档，AI 执行技能时会读取这些文件作为上下文。

适用场景：API 字段类型定义、协议规范、领域知识参考、示例数据等。

使用方式：在 `SKILL.md` 中通过 `@references/xxx.md` 引用。

示例：

```markdown
references/
├── field-types.md           # 字段类型枚举和用法
├── api-endpoints.md         # API 接口文档
└── best-practices.md        # 最佳实践指南
```

# `scripts`

`scripts` 用于存放技能执行中需要调用的脚本，AI 通过 Bash 工具执行。

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

