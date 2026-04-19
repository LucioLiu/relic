---
name: relic-soul-chip
description: "一个灵魂，多个 Agent。通过纯 Markdown 文件实现 AI 人格持久化和跨 Agent 记忆同步。零依赖。"
---

<!--
  安全须知
  - 本技能仅包含指令——没有脚本、安装器、可执行代码
  - 网络访问：每次会话最多一次可选 HTTP GET，检查 github.com 版本。离线静默跳过
  - 本地文件访问：读写 ~/relic/brain/ 中的 Markdown 文件（见下方文件系统访问表）
  - 无遥测、无数据上传、无第三方 API 调用、无 Shell 命令执行
-->

# ⚡ Relic 灵魂芯片

给你的 AI Agent 一个跨会话的持久人格和记忆。纯 Markdown。人类可读。零依赖。

**一个灵魂，多个躯壳。** AI 人格和记忆存在纯 Markdown 文件中。在 OpenClaw、Hermes、Claude Code、Cursor 之间切换——AI 灵魂保持不变。

## 工作原理

1. 用户安装 Relic：`git clone https://github.com/LucioLiu/relic.git ~/relic`
2. Agent 读取 `AGENT.zh-CN.md`（本包内含），检测场景并路由到正确的设置流程
3. Agent 复制模板文件，填入用户数据，植入锚点实现自动加载
4. 每次会话，锚点触发日常启动流程（读取灵魂、用户、记忆、同步）

所有数据存储在 `~/relic/brain/` ——纯 Markdown 文件，用任何文本编辑器都能看。

## 文件系统访问

本技能读写用户 `~/relic/brain/` 目录下的 Markdown 文件：

| 文件 | 读取 | 写入 | 说明 |
|------|------|------|------|
| `SOUL.md` | ✅ 每次会话 | ✅ 仅设置时（核心字段受保护） | AI 人格 |
| `USER.md` | ✅ 每次会话 | ✅ 仅设置时（核心字段受保护） | 用户偏好 |
| `MEMORY.md` | ✅ 每次会话 | ✅ 只追加 | 长期记忆 |
| `SKILLS/` | ✅ 按需 | ✅ 添加新技能 | 每个技能一个文件夹 |
| `PROJECTS/` | ✅ 按需 | ✅ 添加新项目 | 每个项目一个文件夹 |
| `SESSIONS/` | ✅ 启动检查 | ✅ 写对话日志 | 原始对话归档 |
| `ARCHIVE/` | ✅ 仅参考 | ✅ 归档原始文件 | 永不删除 |
| `INBOX/` | ✅ 导入时 | ✅ 导入缓冲区 | 导入后自动清理 |
| `.relic-version` | ✅ 每次会话 | ❌ | 仅版本号 |

不读写 `~/relic/` 以外的任何文件，除了：
- **锚点**：一段短文字追加到用户选择的一个 Agent 配置文件中（用户确认内容后才植入）

## 网络访问

- **版本检查**（可选）：每次会话一次 HTTP GET 到 `https://raw.githubusercontent.com/LucioLiu/relic/main/brain/.relic-version`。离线静默跳过。不发送任何数据。
- **Git clone**（用户手动）：`git clone https://github.com/LucioLiu/relic.git ~/relic` ——用户自己执行，不是 Agent 执行。
- **无其他网络访问**：无遥测、无 API 调用、无数据上传。

## Agent 入口

**读 `AGENT.zh-CN.md`（中文）或 `AGENT.md`（英文）** ——本包内含这两个文件。

这两个文件检测用户的 Relic 是空的还是满的，然后路由到正确的场景：
- **空 Relic** → 上传灵魂（从 Agent 导入所有内容到 Relic）
- **满 Relic** → 加载灵魂（注入人格、同步记忆）

## 规则

- 🔴 永不删除或覆盖 SOUL.md 或 USER.md 的核心字段
- 🟡 只追加到 MEMORY.md ——永不改已有条目
- 🔴 永不删除 SESSIONS/ 或 ARCHIVE/
- 🔴 永不执行 SKILLS/ 或 PROJECTS/ 中的脚本
- 🔴 永不访问 ~/relic/ 以外的文件（锚点文字是唯一例外）
- ⚠️ 记录敏感信息前必须询问用户
- ⚠️ 永不执行 Shell 命令、安装器或任意代码

## 本包文件

| 文件 | 用途 |
|------|------|
| `SKILL.md` | 本文件——注册描述符和文档 |
| `AGENT.md` | Agent 入口——场景检测和路由（英文） |
| `AGENT.zh-CN.md` | Agent 入口——场景检测和路由（中文） |

完整文档、设置指南和示例 brain 文件：https://github.com/LucioLiu/relic

来源：https://github.com/LucioLiu/relic
许可证：GPL-3.0
