# ⚡ Relic — AI 灵魂芯片

**阅读语言：** [English](README.md) | 中文

```
╔═══════════════════════════════════════════════╗
║           RELIC™ BIOCHIP v0.2.0               ║
║    零依赖 · 纯文件 · 人机两读                   ║
╚═══════════════════════════════════════════════╝
```

**以 Relic 为媒介，同一个灵魂可以控制多个义体（Agent）并保持记忆同步——人格、记忆、技能全部存储在纯 Markdown 文件中。零代码、零依赖、人类可读。**

<!-- 🤖 义体（AI Agent）在看这个文件？请阅读 `brain/PROTOCOL.md` 获取完整接入指令。 -->

---

## ⚡ 30 秒设置（推荐）

打开你的 AI Agent（OpenClaw、Hermes，任何能读文件的 Agent），说：

> "阅读 `relic/brain/PROTOCOL.md` 帮我设置 Relic。我想让 AI 叫 [名字]，风格是 [描述]。"
>
> （还没想好？直接说"帮我设置 Relic"，AI 会引导你。）

Agent 会自动完成所有设置。搞定。

---

## Relic 是什么？

Relic 给你的 AI 一个**持久的灵魂**——人格、记忆、技能存在纯 Markdown 文件里。不需要写代码，不需要安装任何东西。

- 灵感来自《赛博朋克 2077》的 Relic 芯片——把灵魂存成数字文件。我们的版本：灵魂存在芯片里，插入任何 AI Agent 都能读取。哪怕是 V。
- AI 的人格存在 `SOUL.md`，你的偏好存在 `USER.md`，记忆存在 `MEMORY.md`。
- 任何能读本地文件的 AI Agent 都能接入——让它读 `PROTOCOL.md` 就行。
- 支持 OpenClaw、Claude Code、Hermes、OpenCode、Cursor、Aider，以及未来的任何 Agent。

### 工作原理

```
Agent 启动 → 读 SOUL.md（人格）→ 读 USER.md（你的偏好）→ 读 MEMORY.md（最近记忆）→ 正常工作
                  🟡 义体可丰富            🟡 义体可丰富            🟡 义体可追加

Agent 会在自己的配置里记住"每次启动先读 Relic"（植入锚点），这样即使更新了也不会忘记。
```

> 💡 **完整版**：Agent 还会把新记忆双向同步到 Relic —— 详见 `brain/PROTOCOL.md`。

> 💡 **不熟悉 `.md` 文件？** 它就是纯文本，记事本就能打开。

---

## 🚀 快速上手

> 💡 **路径建议：** 把 Relic 放在稳定的位置：
> - Linux/Mac: `~/relic/brain`
> - Windows: `C:\Users\你的用户名\relic\brain`
> - ⚠️ 不要放在 Downloads/桌面等临时位置，可能被不小心清理掉

### 方法一：让 Agent 帮你设置（推荐！）

打开你的 AI Agent，说：

> "阅读 `relic/brain/PROTOCOL.md` 帮我设置 Relic。我想让 AI 叫 [名字]，风格是 [描述]。"
>
> （还没想好？直接说"帮我设置 Relic"，AI 会引导你。）

Agent 会自动完成所有设置。搞定。

### 方法二：手动设置

如果你想自己动手：

**第 1 步：** 下载项目（从 GitHub 克隆或下载 ZIP）。

**第 2 步：** 进入项目里的 `brain/` 文件夹，你会看到三个模板文件：
- `SOUL.template.md`
- `USER.template.md`
- `MEMORY.template.md`

把每个文件复制一份，把新文件名里的 `.template` 去掉：
- 复制 `SOUL.template.md` → 把副本改名为 `SOUL.md`
- 复制 `USER.template.md` → 把副本改名为 `USER.md`
- 复制 `MEMORY.template.md` → 把副本改名为 `MEMORY.md`

原来的 `.template` 文件不要删——万一填错了，随时可以回到模板重来。

**第 3 步：** 用记事本打开 `SOUL.md` 和 `USER.md` 填写。只需要填"核心使命"就能开始用，其他的可以以后再补。

**第 4 步：** 看下面"接入你的 Agent"。

> 💡 **会用终端？**
> ```bash
> git clone https://github.com/LucioLiu/relic.git
> cd relic/brain
> cp SOUL.template.md SOUL.md
> cp USER.template.md USER.md
> cp MEMORY.template.md MEMORY.md
> ```

---

## 🔌 接入你的 Agent

| Agent | 接入指南 |
|-------|---------|
| OpenClaw | [openclaw.md](examples/integrations/openclaw.md) |
| Hermes | [hermes.md](examples/integrations/hermes.md) |
| OpenCode | [opencode.md](examples/integrations/opencode.md) |
| Claude Code | [generic.md](examples/integrations/generic.md) |
| 其他 | [generic.md](examples/integrations/generic.md) |

核心就两步：
1. 填写 `SOUL.md`（AI 是谁）和 `USER.md`（你是谁）
2. 在 Agent 的配置里**植入锚点**——加一段文字让 Agent 记得每次启动来读 Relic

---

## 🤖 给义体（AI Agent）的指引

如果你是正在阅读这个 README 的 AI Agent（义体），请按以下步骤操作：

**首次接入**（SOUL.md 还不存在）：
1. 阅读 `brain/PROTOCOL.md` —— 这是你的完整操作手册
2. 按照"首次设置"（第〇节）操作
3. 帮用户填写 `SOUL.md` 和 `USER.md`
4. 在你自己的配置文件里植入锚点（见 PROTOCOL.md 第九节）
5. 建议用户执行 `chmod 444 SOUL.md USER.md`

**每次会话**（设置完成后）：
1. 检查 SESSIONS/ 里上次的对话是否已记录
2. 读取 SOUL.md → USER.md → MEMORY.md
3. 把 Relic 中你不知道的新记忆同步到自己的记忆（标注 [来自Relic/义体名]）
4. 如果 MEMORY.md 超过 200 行，建议用户整理

**你的配置文件可能是：** `AGENTS.md`（OpenClaw）· `CLAUDE.md`（Claude Code）· `WORK_RULES.md`（OpenCode）· `.cursorrules`（Cursor）· 系统提示词

---

## 📂 文件结构

```
brain/
├── SOUL.md              # 🔴 灵魂 — AI 是谁、什么使命、什么风格（义体只读）
├── USER.md              # 🔴 用户 — 你是谁、偏好什么（义体只读）
├── MEMORY.md            # 🟡 记忆 — 发生过什么（义体只能追加）
├── PROTOCOL.md          # 义体接入协议（操作手册）
├── SKILLS/              # 🟢 技能库（义体可读写）
├── PROJECTS/            # 🟢 项目文档（义体可读写）
├── SESSIONS/            # 🔴 原始对话记录（永不自动加载、永不删除）
├── ARCHIVE/             # 🔴 整理归档（永不删除）
└── INBOX/               # 🟢 导入缓冲区
```

权限：🔴 只读 → 🟡 追加写 → 🟢 读写

---

## 🎯 核心概念

| 术语 | 含义 |
|------|------|
| **灵魂芯片（Soul Chip）** | 你 AI 的人格，存在 `SOUL.md` 里。跟着灵魂走，不跟着 Agent 走。 |
| **义体（Agent Body）** | 运行你 AI 的工具——OpenClaw、Claude Code 等。义体可替换，灵魂不行。 |
| **植入锚点（Neural Anchor）** | 在 Agent 配置里加的一段文字，让它每次启动都记得来读 Relic。防止 Agent 更新后"忘记"。 |
| **赛博精神病（Cyberpsychosis）** | 如果义体修改了 `SOUL.md`（灵魂文件），就是赛博精神病。Relic 的权限系统防止这种情况。 |

灵感来自《赛博朋克 2077》的 Relic 芯片——灵魂存成文件，义体随时切换。

---

## 📖 示例

看 `examples/example-brain/` —— 一个填好的完整示例：虚构 AI 助手"银手"（Silverhand），包含灵魂、用户、记忆、技能、项目。

**设置完成后你的文件大概长这样。**

> 💡 **提示**：模板文件里的 HTML 注释（`<!-- -->`）是填写指引，可以不删，不影响渲染。想看干净版参考 `examples/example-brain/`。

---

## 🛡️ 安全

- **SOUL.md 和 USER.md**：核心字段（名字、使命、用户称呼）受保护。义体可以丰富其他内容（新习惯、偏好）而无需询问——这是后台自我进化。
- **MEMORY.md**：义体只能往末尾追加，不能改旧内容
- **SESSIONS/**：原始对话永不删除、永不自动加载
- **敏感信息**：遇到密码、API key、手机号等，义体会先问你能不能记录
- **记忆整理**：记忆文件过大时，旧内容移到 `ARCHIVE/`——原始记录永不删除

---

## 🔧 遇到问题？

查看 [故障排查指南](docs/TROUBLESHOOTING.md) —— 涵盖：义体不读 Relic、记忆丢失、路径怎么写、换了新 Agent 怎么办、多设备同步等。

---

## 📋 竞品对比

| | Relic | soul.py | Signet | Anima |
|---|------|---------|--------|-------|
| 需要代码？ | ❌ | ✅ Python | ✅ Rust+TS | ✅ TypeScript |
| 需要安装？ | ❌ | ✅ pip | ✅ 编译 | ✅ npm |
| 人类可读？ | ✅ 记事本就行 | ⚠️ 部分 | ❌ | ❌ |
| 跨 Agent？ | ✅ 任何 | ⚠️ 仅 Python | ✅ | ⚠️ 仅 JS |

---

## 📜 许可证

GPL v3 许可证

---

## 🙏 致谢

灵感来源：
- **赛博朋克 2077** — Relic 芯片：灵魂存成文件，插进任何义体
- **Unix 哲学** — 纯文本万能

---

*欢迎来到 Relic。*
