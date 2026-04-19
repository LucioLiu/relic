# ⚡ Relic — AI 灵魂芯片

**阅读语言：** [English](README.md) | 中文

```
╔═══════════════════════════════════════════════╗
║           RELIC™ 灵魂芯片 v1.1.1             ║
║    零依赖 · 纯文件 · 人类可读                 ║
║        经历过真实工作流考验                     ║
╚═══════════════════════════════════════════════╝
```

**Relic 让你的 AI 拥有一个跨工具通用的持久灵魂。** 性格、记忆、技能、项目知识——全部存在纯文本文件里。支持 OpenClaw、Claude Code、Hermes、Cursor、Aider，或者任何能读文件的 AI 工具。零代码、零安装、零依赖。

---

## 👇 先选一个：

- 🤖 **"我是 AI Agent"** → 跳到[给 AI Agent 看的](#-给-ai-agent-看的部分)
- 👤 **我是人类** → 继续往下读

---

## Relic 是什么？

Relic 是一个装满文本文件的文件夹，存着你 AI 的性格和记忆。你可以把它想象成 AI 灵魂的 U 盘——插到任何 AI 工具上，那个工具立刻就知道你的 AI 叫什么、你喜欢什么、你们一起做过什么。

**里面有什么（全在 `brain/` 文件夹里）：**
- `SOUL.md` — AI 的性格、价值观和使命
- `USER.md` — 你的偏好、习惯和沟通方式
- `MEMORY.md` — 最近发生了什么（对话、决策、经验教训）
- `SKILLS/` — AI 学到的可复用技能和工作流
- `PROJECTS/` — 正在进行的项目文档
- `SESSIONS/` — 原始对话记录（永久保存）
- `ARCHIVE/` — 整理归档（记忆太长时移到这里，原始记录永不删除）

**核心理念：** 你用的每一个 AI 工具都读写同一套文件。OpenClaw 写了一条记忆 → Claude Code 下次会话就能读到。不需要 API，不需要云服务，不需要同步工具——就是你电脑上的文件。

> 💡 灵感来自《赛博朋克 2077》的 Relic 芯片——荒坂集团的「守护你的灵魂」项目：将人类意识转化为数字印迹，存储在生物芯片上。插到任何躯壳里，人格就活过来了。我们把这套概念用在了 AI Agent 身上。

---

## 🚀 设置指南

### 你想怎么设置？

- 🤝 **"让 AI 帮我搞"**（推荐）→ 看下面的 Step 1
- ✋ **"我自己来"** → 跳到[手动设置](#-手动设置自己来)

### 第一步：下载 Relic

首先，把 Relic 文件夹下载到你的电脑上。

**如果你知道怎么用终端/命令行**，运行：
```
git clone https://github.com/LucioLiu/relic.git ~/relic
```

**如果上面那句话看不懂**——没关系！下载 ZIP 文件就行：
1. 点这个链接：[下载 Relic ZIP](https://github.com/LucioLiu/relic/archive/refs/heads/main.zip)
2. 解压 ZIP 文件
3. 把 `relic` 文件夹放到你找得到的地方，比如你的用户目录：
   - Mac：`/Users/你的名字/relic/`
   - Windows：`C:\Users\你的名字\relic\`
   - Linux：`/home/你的名字/relic/`

> 💡 选一个固定的位置——这是你 AI 的永久住所。别放下载文件夹或桌面。

### 第二步：告诉最了解你的 AI 来设置

打开那个**最了解你**的 AI 工具——跟你聊得最多的那个。然后说：

> "读一下 `~/relic/brain/PROTOCOL.md`，把你知道的关于我的一切导入 Relic。"

你的 AI 会带你走完剩下的流程。它会问你问题、填写文件、设置好一切。

等设置全部完成后再连接其他 AI 工具。

### 第三步：一个一个连接其他 AI 工具

对于每个额外的 AI 工具（顺序随意），告诉它：

> "读一下 `~/relic/brain/PROTOCOL.md`，帮我设置 Relic。"

**验证每一个**：问"我的 AI 叫什么名字？我叫什么？"——两个都要答对。答对了再连下一个。

### 第四步：搞定！🎉

从现在起每次会话都自动启动。你的 AI 工具共享灵魂，记忆双向同步，所有内容都存在你掌控的纯文本文件里。

> 💡 **同步原理**：每个 AI 工具都读写同一套 Relic 文件。新会话开始时，工具会读取全部七大记忆文件来补课。但同步只在新会话开始时发生——如果你对话到一半切换工具，当前对话还不会自动进到 Relic。需要立刻转接？告诉当前 AI：「请把本次对话的关键信息写入 Relic。」

---

<details>
<summary>🔧 手动设置（自己来）</summary>

不需要 AI 帮忙。操作步骤：

1. **打开 `brain/` 文件夹**（在下载的 `relic` 文件夹里面）
2. **复制模板文件**（模板文件名里有 `.template`，就是给你照着填的空表格）：
   - `SOUL.template.md` → 复制并改名为 `SOUL.md`
   - `USER.template.md` → 复制并改名为 `USER.md`
   - `MEMORY.template.md` → 复制并改名为 `MEMORY.md`
3. **用任何文本编辑器打开 `SOUL.md`**（记事本、TextEdit、VS Code 都行），至少填好「核心使命」部分
4. **打开 `USER.md`**，填上你的偏好
5. **（仅 Mac/Linux）锁定文件**防止误修改：
   ```
   chmod 444 SOUL.md USER.md
   ```
   这句话的意思是"给这两个文件上把锁，防止任何程序（包括你的 AI）不小心改了它们。就像给日记本上了个挂锁。" 以后你自己想改的话，先解锁就行。Windows 用户可以跳过这步。
6. **把你的 AI 工具指向** `brain/PROTOCOL.md`——它会接管剩下的

</details>

---

## 🔌 你在用哪个 AI 工具？

| AI 工具 | 怎么连接 |
|---------|---------|
| OpenClaw | 看 `examples/integrations/openclaw.md` |
| Hermes | 看 `examples/integrations/hermes.md` |
| OpenCode | 看 `examples/integrations/opencode.md` |
| Claude Code | 看 `examples/integrations/generic.md` |
| Cursor | 看 `examples/integrations/generic.md` |
| 其他工具 | 看 `examples/integrations/generic.md` |

所有指南的模式都一样：把你的 AI 指向 `brain/PROTOCOL.md`，它自己搞定剩下的。

---

## 🤖 给 AI Agent 看的部分

如果你是正在读这段话的 AI Agent，你需要做这些：

**第一次连接**（SOUL.md 还不存在）：
1. 读 `brain/PROTOCOL.md`——那是你的完整操作手册
2. 按「首次设置」（第 〇 节）操作
3. 帮用户填好 `SOUL.md` 和 `USER.md`
4. 在你自己的配置文件里植入神经锚点（见 PROTOCOL.md 第九节）
5. 建议用户运行 `chmod 444 SOUL.md USER.md`——这会锁定文件防止误修改

**每次会话**（设置完成后）：
1. 检查 `SESSIONS/` 有没有遗漏的对话记录
2. 读 `SOUL.md` → `USER.md` → `MEMORY.md` → 扫描 `SKILLS/` 和 `PROJECTS/`
3. 把 Relic 中的新记忆同步到自己的记忆文件（标注 [fromRelic/躯壳名]）
4. 把新记忆写回 Relic（双向同步）
5. 如果 `MEMORY.md` 超过 200 行，建议整理

**你的配置文件**（锚点写在这里）：
- OpenClaw → `AGENTS.md`
- Claude Code → `CLAUDE.md`
- Hermes → 配置文件或 prompt 模板
- OpenCode → `WORK_RULES.md` 或 instructions
- Cursor → `.cursorrules`

---

## 📂 文件结构

```
brain/
├── SOUL.md              # 🟡 灵魂——AI 是谁（躯壳可丰富，核心字段受保护）
├── USER.md              # 🟡 用户——你是谁（躯壳可丰富，核心字段受保护）
├── MEMORY.md            # 🟡 记忆——发生了什么（只能追加，不能改旧内容）
├── PROTOCOL.md          # 躯壳接入协议（操作手册）
├── SKILLS/              # 🟢 技能库（可读写）
├── PROJECTS/            # 🟢 项目文档（可读写）
├── SESSIONS/            # 🔴 原始对话记录（永不删除）
├── ARCHIVE/             # 🔴 整理归档（永不删除）
└── INBOX/               # 🟢 导入缓冲区
```

权限级别：🔴 只读 → 🟡 可丰富（核心受保护）/ 追加写 → 🟢 读写

> 💡 **关于 SKILL.md 文件**：项目根目录有两个 SKILL.md——`SKILL.md`（给 Hermes/agentskills.io 平台用）和 `skill/SKILL.md`（给 ClawHub 平台用）。这些是**平台接入说明**，不是你 AI 的实际技能。你 AI 真正学到的技能存在 `brain/SKILLS/` 里。

---

## 🎯 核心概念

| 术语 | 含义 |
|------|------|
| **灵魂** | AI 的性格，存在 `SOUL.md` 里。跨工具通用。 |
| **躯壳** | 运行 AI 的工具——OpenClaw、Claude Code 等。躯壳可以换，灵魂不能丢。 |
| **神经锚点** | 写在你 AI 工具配置文件里的一小段文字，告诉它每次会话都要读 Relic。防止 AI 更新后"忘记"Relic。 |
| **双向同步** | AI 既从 Relic 读取，也把新记忆写回 Relic。所有连接的工具保持同步。 |
| **赛博精神病** | 修改 `SOUL.md` 的核心字段（名字、使命）——Relic 的权限系统会保护这些字段。Agent *可以*丰富 SOUL.md（新增习惯和偏好）——那是健康的自我进化，不是赛博精神病。 |

---

## 📖 示例

看 `examples/example-brain/` 里的完整示例——一个叫"银手 (Silverhand)"的虚构 AI 助手，包含灵魂、用户、记忆、技能、项目、对话记录和归档文件。

**这展示了你设置完成后文件应该长什么样。**

> 💡 模板文件里有 HTML 注释（`<!-- -->`）作为填写指引，不影响使用。想看干净的版本，看 `examples/example-brain/`。

---

## 🛡️ 安全

- **SOUL.md 和 USER.md**：核心字段（名字、使命、用户称呼）受保护。Agent 可以丰富其他内容（新习惯、偏好），这是健康的自我进化
- **MEMORY.md**：只能在末尾追加，永远不能改旧内容
- **SESSIONS/**：原始对话永不删除，启动时不自动加载
- **敏感信息**：Agent 会先问你才记录密码、API key、手机号等
- **记忆整理**：记忆文件变大时，旧内容移到 `ARCHIVE/`——原始记录永不删除

---

## 🔧 遇到问题？

看 `docs/TROUBLESHOOTING.md`——覆盖：Agent 不读 Relic、记忆丢失、路径格式、切换工具、多设备同步等。

---

## 📜 许可证

GPL v3 许可证

---

## 🙏 致谢

作者：[LucioLiu](https://github.com/LucioLiu) · 源码：[github.com/LucioLiu/relic](https://github.com/LucioLiu/relic)

灵感来源：
- **《赛博朋克 2077》** — 荒坂集团 Relic 芯片：「守护你的灵魂」——意识存成数字文件
- **Unix 哲学** — 纯文本永不过时

---

*欢迎来到 Relic。*
