---
name: relic-soul-chip
description: "一个灵魂，多个 Agent。通过纯 Markdown 文件实现 AI 人格持久化和跨 Agent 记忆同步。零依赖。"
---

<!--
  安全须知
  - 本技能仅包含指令——没有脚本、安装器、可执行代码
  - 网络访问：每次会话最多一次可选的只读 HTTP 请求检查版本。不会发送或下载任何数据。
  - 本地文件访问：Agent 读取 ~/relic/brain/ 中的 Markdown 文件。始终对用户可见，敏感内容需用户确认
  - 无遥测、无数据上传、无第三方 API 调用、无 Shell 命令执行
-->

# ⚡ Relic 灵魂芯片

> **🤖 AI Agent？读仓库根目录的 `AGENT.zh-CN.md`（中文）或 `AGENT.md`（英文）。** 那里面有完整的分步指引。本文件是注册描述符，不包含执行步骤。

一个灵魂，多个躯壳。你的 AI 人格和记忆存在纯 Markdown 文件中。在 OpenClaw、Hermes、Claude Code 之间切换——AI 灵魂保持不变。

## 快速开始

**Agent**：读仓库根目录的 `AGENT.zh-CN.md`（中文）或 `AGENT.md`（英文），按步骤执行。

**人类**：读 `README.md` 了解设置说明。

## 规则

- 🔴 永不删除或覆盖 SOUL.md 或 USER.md 的核心字段
- 🟡 只追加到 MEMORY.md
- 🔴 永不删除 SESSIONS/ 或 ARCHIVE/
- 🔴 永不执行 SKILLS/ 或 PROJECTS/ 中的脚本
- ⚠️ 记录敏感信息前必须询问

来源：https://github.com/LucioLiu/relic
