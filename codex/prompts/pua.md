---
description: "PUA router for Codex. Use `/prompts:pua` for core mode, or `/prompts:pua p7|p9|p10|pro|yes|en|ja` to switch to a Codex-ready variant."
argument-hint: "[p7|p9|p10|pro|yes|en|ja|loop]"
---

根据 `$ARGUMENTS` 选择并调用对应的 Codex skill：

- 无参数：调用 `pua`
- `p7`：调用 `p7`
- `p9`：调用 `p9`
- `p10`：调用 `p10`
- `pro`：调用 `pro`
- `yes`：调用 `yes`
- `en` 或 `pua-en`：调用 `pua-en`
- `ja` 或 `pua-ja`：调用 `pua-ja`

如果参数是 `loop` 或 `pua:loop`：
- 不要假装 loop 已在 Codex 中可用
- 明确说明：`loop` 依赖 Claude 的 hooks 和 `.claude` 状态文件，当前 Codex 版本不支持自动迭代回灌
- 引导用户改用 `pua`、`pro`，或手动分阶段推进任务

如果模式参数后面还带了任务描述，把剩余文本当作用户上下文一并传给目标 skill。

调用目标 skill 后，严格按该 skill 的协议执行。
