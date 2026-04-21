# Relic — 项目总计划（最终版）

> 名称灵感：赛博朋克 2077 · Arasaka Relic Biochip
> 灵魂芯片，插入任何躯壳都能运转。

---

## 一句话定义

Relic 是一个零依赖、纯文件、人机两读的 AI 人格持久化框架。
任何 AI Agent 照着协议读一遍就能接入，不需要写代码。

---

## 核心理念

```
Relic 芯片 = 灵魂 + 记忆 + 技能
躯壳(Agent) = 执行 + 工具

Relic 不依赖任何特定 Agent 框架
Agent 是可替换的躯壳，Relic 是唯一的灵魂
```

你（用户）有一个灵魂芯片（Relic），里面存着你的人格、记忆、偏好。
你可以把这个芯片插入任何一个躯壳（OpenClaw、Hermes、Claude Code、OpenCode……），
躯壳获得灵魂后为你工作。换躯壳不换灵魂。

---

## 设计原则

### 1. 约定大于配置
文件名就是约定：SOUL.md = 灵魂，USER.md = 用户，MEMORY.md = 记忆。

### 2. Markdown 原生
人类直接编辑，Agent 直接读取。cat SOUL.md 就能看灵魂。

### 3. 三级权限分离（防赛博精神病）
| 权限 | 文件 | 躯壳能做什么 |
|------|------|------------|
| 🟡 可丰富（核心受保护） | SOUL.md, USER.md | 可以新增内容但禁止修改核心字段（名字、使命、用户称呼） |
| 🔴 只读 | ARCHIVE/, SESSIONS/ | 只能读，永远不能修改或删除 |
| 🟡 追加写 | MEMORY.md | 只能在末尾追加，不能改旧的 |
| 🟢 读写 | SKILLS/, PROJECTS/ | 可以添加和更新 |

### 4. Append-only 记忆
不修改历史，只追加。定期压缩归档，原始记录永不删除。

### 5. 渐进式加载（6层）
```
L0 灵魂（每次必加载，~1K tokens）：SOUL.md + USER.md
L1 记忆（启动时加载，~2-8K tokens）：MEMORY.md 末尾 N 条
L2 技能（按需加载）：SKILLS/ 中相关技能
L3 项目（按需加载）：PROJECTS/ 中相关项目文档
L4 归档（按需查）：ARCHIVE/ 压缩记忆
L5+ 对话（永不自动加载）：SESSIONS/ 完整对话记录
```

### 6. 躯壳植入锚点（核心！）
在躯壳自己的核心配置文件里植入锚点，确保躯壳每次启动都记得来找 Relic。
这是整个系统能运转的前提——躯壳忘了我们，一切白搭。

### 7. 中英双语
文件名英文（躯壳好引用），内容双语（人人可读）。UI 支持中英切换。

---

## 核心文件结构

```
brain/
├── SOUL.md                  # 🟡 可丰富（核心受保护）— 灵魂（含核心使命）
├── USER.md                  # 🟡 可丰富（核心受保护）— 用户画像
├── MEMORY.md                # 🟡 追加写 — 精炼记忆
├── PROTOCOL.md              # 躯壳接入协议（中文版）
├── PROTOCOL.en.md           # 躯壳接入协议（English）
├── .relic-version           # 版本号
├── SKILLS/                  # 🟢 读写 — 技能库（YAML Front Matter 元数据）
│   └── *.md
├── PROJECTS/                # 🟢 读写 — 项目文档（躯壳或用户添加）
│   └── *.md
├── SESSIONS/                # 🔴 只读 — 原始对话记录（永不自动加载）
│   ├── 2026-04/
│   │   ├── 2026-04-15.openclaw.md
│   │   └── 2026-04-16.opencode.md
│   └── ...
├── ARCHIVE/                 # 🔴 只读 — 压缩归档（永不删除）
│   ├── 2026-04.raw.md
│   └── index.md
└── INBOX/                   # 🟢 读写 — 导入缓冲区
```

---

## 三大融合场景

### 场景 A：导入（空 Relic + 有记忆的躯壳）
完整搬家——不只是记忆，技能、对话、项目都要搬。
1. 盘点 — 躯壳扫描自己的所有持久化内容，列清单给用户确认
2. 导入记忆 → MEMORY.md（按时间戳排序，敏感信息主动询问）
3. 导入技能 → SKILLS/（排除躯壳平台专属工具）
4. 导入对话 → SESSIONS/（原始内容不改不摘要）
5. 导入项目 → PROJECTS/（从记忆和对话中识别）
6. 清理与确认 — 精度校验（原始字节vs转换后字节，超50%警告）、原文归档到ARCHIVE/raw/（永不删除）、汇报导入统计

### 场景 B：注入（有 Relic + 空躯壳）
B-0. 自检：评估躯壳存储能力，选择搬运策略
B-1. 执行启动流程（读 SOUL/USER/MEMORY，同步新记忆到自身）
B-2. 灵魂注入：SOUL.md 写入躯壳核心配置（优先级：核心身份 > 行为规范 > 详细设定）
B-3. 同步 Relic 内容（记忆/技能/项目，逐项核对）
B-4. 校验与汇报：覆盖率检查 + 向用户列出同步清单

空 Relic + 空躯壳时：问用户一个选择——
  [A] 从零养成：自己描述，躯壳帮填
  [B] 按躯壳默认来：导入躯壳自带人设

### 场景 C：融合（有 Relic + 有记忆的躯壳）
三选一，不搞复杂的重合度计算：
  [1] 保留 Relic 灵魂（只导入躯壳记忆）
  [2] 保留躯壳灵魂（替换 Relic 灵魂）
  [3] 融合 — 躯壳生成预览报告，列出关键差异，用户逐条选择

---

## 记忆压缩方案

双线制：
- **软线 8K tokens**：超过时提醒，允许继续
- **硬线 16K tokens**：超过时必须压缩

压缩流程：
1. 把 MEMORY.md 整体移入 ARCHIVE/YYYY-MM.raw.md（原始保留）
2. 躯壳提炼生成精简版 MEMORY.md
3. 更新 ARCHIVE/index.md

SESSIONS/（原始对话）永不压缩、永不自动加载。用户可选保留时长（永久/1年/6个月/3个月），默认永久。空间不是问题——一年对话约72MB，比十张照片小。

---

## 单文件导出

导出 .relic 文件（zip打包）时，三级蒸馏：

| 级别 | 包含内容 | 适合场景 |
|------|---------|---------|
| 灵魂模式 | SOUL.md + USER.md + MEMORY.md | 公开分享 |
| 标准模式 | 灵魂 + 技能 + 项目 | 迁移设备 |
| 完整模式 | 含 SESSIONS/ 全部 | 完整备份（⚠️隐私提醒） |

---

## 躯壳植入锚点指南

接入 Relic 后，必须在躯壳自己的核心配置文件里植入锚点。完整锚点模板见 `docs/protocol.zh-CN.md` 第九节。

不同躯壳的植入锚点位置：
- OpenClaw → AGENTS.md
- Claude Code → CLAUDE.md
- Hermes → 配置文件或 prompt 模板
- OpenCode → WORK_RULES.md 或 instructions

---

## 竞品分析

| 项目 | ⭐ Stars | 依赖 | 与 Relic 的区别 |
|------|---------|------|---------------|
| agentmemory | 1,602 | TypeScript + MCP | 只做记忆不做灵魂 |
| Signet | 85 | Rust+TS daemon | 需要编译安装 |
| soul.py | 51 | Python | 需要写代码 |
| agent-soul | 4 | Python + Git | 需要运行时 |
| Anima | 4 | TypeScript npm | 需要 npm install |

**Relic 差异化**：零代码、零依赖、纯文件、cat 就能读。市场远未饱和。

---

## 开发路线图

### Phase 1：骨架搭建（当前）
- [x] 确定项目名：Relic
- [x] 确定核心设计原则
- [x] 三方讨论完成（OpenClaw + Hermes + Atlas）
- [x] 确定文件结构和加载层级
- [x] 确定三大融合场景
- [x] 确定记忆压缩方案
- [x] 编写 PROTOCOL.md（中英双语）
- [x] 编写模板文件（中英双语）
- [x] 编写本计划文档
- [x] ~~创建 .relic-manifest.yaml 模板~~（v0.1.0 已删除，v0.2 再考虑）
- [x] 编写 README.md（双语版已完成）

### Phase 2：工具层
- [ ] npx relic init — 一键初始化
- [ ] npx relic ui — Web 管理界面（2077风格）
- [ ] npx relic export — 单文件导出（三级蒸馏）
- [ ] npx relic compress — 手动触发记忆压缩

### Phase 3：验证
- [ ] OpenClaw 实际接入测试（植入锚点+同步）
- [ ] OpenCode 实际接入测试
- [ ] Hermes 接入测试
- [ ] 跨躯壳记忆共享验证

### Phase 4：Skill 上架 + GitHub 发布
- [ ] ClawHub skill（OpenClaw 一行安装）
- [ ] Skill.Fish（Claude Code 一行安装）
- [ ] GitHub 仓库初始化
- [ ] 英文 README
- [ ] 发布 v0.1.0

---

## 讨论记录

本计划由以下讨论催生：
- **OpenClaw（龙虾）**：提出 .chang/brain/ 架构（JSON格式、渐进式加载），贡献了"北极星/核心使命"概念、YAML Front Matter 技能元数据、.relic-manifest.yaml 索引方案，提醒了过度设计风险
- **Hermes（爱马仕）**：提出三层架构和群聊协议，贡献了"融合预览报告"概念、躯壳能力分级思路、自描述文件建议，指出了长期格式寿命和版本迁移隐患
- **Atlas（OpenCode）**：综合两方意见，确定"轻量+Markdown+零代码"方向，提出三级权限、三大融合场景、躯壳植入锚点机制、SESSIONS/原始对话保留，命名 Relic

最终决策权：话寻常（弟弟）

---

## v1.1.1 更新（2026-04-18）

基于 OpenClaw 真实测试 v1.0.4 发现的 27 个问题，进行全面更新。

### 概念升级
- 从"插入=获得灵魂，拔出=出厂重置" → "中央大脑 + 双向同步"
- 每个 Agent 既是读者也是写入者——只加不减（G-Set）
- 锚点从"可选"改为"强烈推荐 + 告知不植入的后果"

### PROTOCOL 重构
- PROTOCOL.md：864 → 475 行（精简，无信息丢失）
- PROTOCOL.en.md：823 → 475 行（与中文版对等）
- SESSIONS 描述："永不自动加载" → "必须创建和写入，启动时不自动读取"

### README 重写
- 完全重写为小白友好决策树（人类/Agent 分支）
- 前 30 行无未解释的技术术语
- 删除竞品对比表
- chmod 加人话解释
- 所有 6 种文件类型都描述（不再只提 3 种）

### 权限标签修复
- SOUL.md 和 USER.md 统一为 🟡（可丰富，核心受保护）
- INBOX/README "删除"矛盾修复 → 移到 ARCHIVE/raw/ 永久保存

### 双语覆盖
- 所有非记忆文件补齐双语版本
- 约 15 个新建或更新的双语文件

### example-brain 扩展
- 新增 SKILLS/、PROJECTS/、SESSIONS/、INBOX/ 及银手风格示例
- 各目录 README 添加防呆说明

### 版本统一
- 所有版本字符串统一到 1.2.0（1.1.1 的历史见 v1.1.1 更新段落；1.2.0 已取代）
