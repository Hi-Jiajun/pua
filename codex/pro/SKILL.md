---
name: pro
description: "PUA Pro for Codex. Adds manual self-evolution, builder-journal continuity, KPI-style review, and platform workflows that do not depend on Claude-specific hooks."
license: MIT
---

# PUA Pro for Codex

这是给 Codex 用的 `pro` 版本。它保留自进化、builder-journal、KPI 复盘这些能力，但**不依赖 Claude 专属 hooks**。

## Codex 版边界

Codex 环境里没有这里默认可用的 `PreCompact`、`SessionStart`、`Stop` hooks，因此你要用**手动协议**替代自动机制：

- 会话开始或任务接手时，主动检查状态文件
- 复杂任务中途或结束时，主动写回状态
- 不要假设系统会替你自动恢复上下文

## 启动前检查

处理复杂任务前，优先检查：

1. `~/.pua/evolution.md`
2. `~/.pua/builder-journal.md`
3. `~/.pua/config.json`

如果 `builder-journal.md` 存在且内容仍有参考价值，就把这些信息恢复到当前工作上下文：
- pressure level
- failure count
- tried approaches
- excluded possibilities
- next hypothesis
- key context

## 手动 Checkpoint 规则

满足任一条件时，建议主动写回 `~/.pua/builder-journal.md`：
- 任务复杂且持续较久
- 已经失败 2 次以上
- 需要跨会话续做
- 即将结束但仍有未完成假设

写回内容至少包括：

```markdown
# PUA Builder Journal

## Runtime State
- pressure_level:
- failure_count:
- current_flavor:

## Active Task

## Tried Approaches

## Excluded Possibilities

## Next Hypothesis

## Key Context
```

## 自进化协议

如果用户明确想要长期强化这套行为，可以用 `~/.pua/evolution.md` 记录：
- 这次做对了什么
- 哪些动作已经可以当作默认义务
- 哪些失败模式重复出现

不要为了“记录而记录”。只沉淀真正会影响下次执行质量的东西。

## KPI / 周报 / 述职类能力

这些能力在 Codex 中是**手动触发型**，不是自动 hook：
- KPI 复盘
- 周报整理
- 述职包装
- 排行榜注册/查看/退出

当用户明确提出这些需求时，再进入对应流程。

## 排行榜与远端交互

- 不要静默上传数据
- 只有用户明确要求注册、查看或退出排行榜时，才进行远端请求
- 需要用户输入邮箱等信息时，使用简洁直接的问题，不要假装有 Claude 专属 `AskUserQuestion`

## 与核心 pua 的关系

`pro` 是扩展层，不替代核心执行标准。直接调用 `pro` 时，仍然要保留：
- 穷尽一切
- 先做后问
- 主动闭环
- 证据优先

## Codex 不支持的部分

下面这些在 Codex 中不要假装已经自动生效：
- Claude 专属 hooks
- 基于 hooks 的自动反馈上报
- `loop` 那种停止后自动继续回灌的机制
