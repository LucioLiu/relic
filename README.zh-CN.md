# 👤 Relic — AI 灵魂芯片（人类版）

> **🤖 你是 AI Agent？** → 这个文件不是给你的。去读 [`AGENT.zh-CN.md`](AGENT.zh-CN.md)

**Read this in:** [English](README.md) | 中文

```
╔═══════════════════════════════════════════════╗
║           RELIC™ BIOCHIP v1.3.2               ║
║    零依赖 · 纯文件 · 人类可读                   ║
╚═══════════════════════════════════════════════╝
```

**Relic 让你的 AI 拥有跨工具的持久灵魂。** 性格、记忆、技能——全部存在纯文本文件里。支持 OpenClaw、Claude Code、Hermes、Cursor、Aider，或任何能读文件的 AI。零代码、零安装、零依赖。

> 💡 灵感来自《赛博朋克 2077》的 Relic 芯片——将意识存成数字文件，插到任何躯壳里，人格就活过来了。

---

## 它能干什么？

**你每换一个 AI 工具，就要重新教它你是谁。** OpenClaw 记得一套，Hermes 记得另一套，互不相通。

**Relic 解决这个问题。** 一个文件夹，纯文本，所有 AI 工具共享同一份灵魂和记忆。不是云服务，不是 API，就是你电脑上的几个 Markdown 文件。

## 里面有什么（全在 `brain/` 文件夹里）

- `SOUL.md` — AI 的性格、价值观和使命
- `USER.md` — 你的偏好、习惯和沟通方式
- `MEMORY.md` — 结构化长期记忆（偏好、决策、经验——提炼过的知识，不是原始聊天）
- `SKILLS/` — AI 学到的可复用技能
- `PROJECTS/` — 进行中或已完成的计划文档
- `SESSIONS/` — 与用户的完整原始对话日志（永久保存）
- `ARCHIVE/` — 归档（记忆太长时移到这里，原始记录永不删除）

---

## 🚀 设置指南

### 你想怎么搞？

- 🤝 **"让 AI 帮我搞"**（推荐）→ 看下面
- ✋ **"我自己来"** → 跳到 [`docs/manual-setup.zh-CN.md`](docs/manual-setup.zh-CN.md)

### 第一步：下载 Relic

**会用终端的**，运行：
```
git clone https://github.com/LucioLiu/relic.git ~/relic
```

**不会终端的**：[下载 ZIP](https://github.com/LucioLiu/relic/archive/refs/heads/main.zip)，解压到你能找到的地方（比如用户目录）。别放桌面或下载文件夹。

### 第二步：让最了解你的 AI 来设置

打开跟你聊得最多的 AI，然后说：

> "读一下 `AGENT.zh-CN.md`，把你知道的关于我的一切导入 Relic。"

它会带你走完剩下的流程。等它全部完成后再连其他工具。

### 第三步：一个一个连接其他 AI 工具

对于每个额外的 AI 工具，告诉它：

> "读一下 `AGENT.zh-CN.md`，帮我设置 Relic。"

AI 会自动判断：如果 Relic 是空的就执行导入，如果已有数据就执行注入（读取灵魂、同步记忆、植入锚点）。

**验证每一个**：问"我的 AI 叫什么名字？我叫什么？"——两个都答对才算通过。

### 第四步：搞定 🎉

从此每次会话自动启动。你的 AI 工具共享灵魂，记忆双向同步。

---

## 🔌 你在用哪个 AI 工具？

| AI 工具 | 怎么连接 |
|---------|---------|
| OpenClaw | `examples/integrations/openclaw.zh-CN.md` |
| Hermes | `examples/integrations/hermes.zh-CN.md` |
| Claude Code | `examples/integrations/generic.zh-CN.md` |
| Cursor | `examples/integrations/generic.zh-CN.md` |
| 其他 | `examples/integrations/generic.zh-CN.md` |

---

## 🛡️ 安全

- `SOUL.md` 和 `USER.md` 核心字段受保护，AI 不可删除
- `MEMORY.md` 只能追加，不能改旧内容
- `SESSIONS/` 永不删除
- 敏感信息（密码、手机号等）录入前必须征得你同意
- 所有数据在你本地，不上传任何地方
- **已知边界**：技能文件可能因平台工具格式不同而无法直接跨平台使用。Relic 同步的是技能描述，不是平台专属实现。

---

## 📖 更多

- [手动设置指南](docs/manual-setup.zh-CN.md)
- [故障排查](docs/TROUBLESHOOTING.zh-CN.md)
- [完整协议参考](docs/protocol.zh-CN.md)（给 AI 看的，人类好奇也可以读）

## 📜 许可证

GPL v3 · 作者 [LucioLiu](https://github.com/LucioLiu) · 源码 [GitHub](https://github.com/LucioLiu/relic)

---

*Welcome to Relic.*
