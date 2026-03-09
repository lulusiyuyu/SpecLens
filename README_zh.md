[English](./README.md)

# SpecLens

> 把任何代码库变成人类可理解、Agent 可消费的分层规格文档。

**Specs 是下一层抽象。Agent 是这层抽象的编译器。**

```
传统开发：  人类 → 代码 → 产品
SpecLens： 人类 → Specs → Agent → 代码 → 产品
```

SpecLens 是一套 **Skills / Prompt 模板系统** —— 一组结构化 Markdown 文件，可以直接喂给任何 AI Coding Agent 使用。零依赖、零安装、Agent-Agnostic、适用于任何 LLM。

---

## 快速开始（30 秒）

**1. 下载**
```bash
git clone https://github.com/lulusiyuyu/SpecLens.git
```

**2. 喂给你的 Agent**

将 AI Agent（Claude Code、Copilot、Cursor、Windsurf、Gemini CLI 等）指向 `skills/` 目录，然后说：

> "使用 Analyze skill 分析我的项目 `/path/to/my-project`"

**3. 浏览 Specs**

Agent 会生成一个镜像你项目结构的 Specs 文件夹——从宏观概览到微观模块 Spec。先读顶层文件，再按需深入。

---

## 它能做什么？

| 问题 | SpecLens 如何解决 |
|------|-----------------|
| 学习大型代码库很痛苦 | 自动生成分层 Specs：宏观→微观，按需展开 |
| AI Agent 容易偏离意图 | Specs 作为明确的意图文档指导 Agent |
| 文档容易腐化 | Specs 既是文档，又是代码变更的上游源 |
| AI 生成的代码难以调试 | Specs 镜像源码结构——快速定位和理解 |

---

## 三种使用模式

### 🔍 学习模式 — 逆向工程
```
代码库 → [Analyze] → Specs 骨架 → 浏览顶层
                                 → [Expand] → 深入任意模块
```
*几分钟理解一个项目，而不是几天。*

### 🏗️ 开发模式 — 正向工程
```
你的想法 → 编写 Specs → [Code from Spec] → Agent 生成代码
                                         → [Validate] → 一致性检查
```
*写规格，不写代码。让 Agent 来编译。*

### 🔄 维护模式 — 迭代演进
```
Specs v1 → 修改 Specs → Specs v2
         → [Diff & Upgrade] → 识别意图变更 → Agent 修改代码
```
*改 Spec，不改代码。Review Spec diff，不 Review 代码 diff。*

---

## Skills 一览

| Skill | 描述 |
|-------|------|
| **[Analyze](skills/analyze/SKILL.md)** | 逆向分析代码库，生成镜像结构的 Specs 文件夹骨架 |
| **[Expand](skills/expand/SKILL.md)** | 将骨架 Spec 展开为详细规格 |
| **[Validate](skills/validate/SKILL.md)** | 检查 Specs 之间以及 Specs 与代码之间的一致性 |
| **[Diff & Upgrade](skills/diff-upgrade/SKILL.md)** | 检测 Specs 变更，生成代码修改任务列表 |
| **[Code from Spec](skills/code-from-spec/SKILL.md)** | 从 Spec 文件生成代码和测试 |

---

## 示例 Specs（真实项目）

浏览从真实开源项目生成的 Specs：

| 项目 | 语言 | 描述 | Specs |
|------|------|------|-------|
| **OpenHands** | Python | AI 软件工程 Agent 平台 | [examples/openhands/](examples/openhands/) |
| **OpenCode** | Go | 终端原生 AI 编码 Agent | [examples/opencode/](examples/opencode/) |
| **claude-code** | TypeScript | Claude Code 插件生态 | [examples/claude-code/](examples/claude-code/) |
| **SpecLens** | Markdown | 本项目自身（Dogfooding） | [examples/speclens-self/](examples/speclens-self/) |

从任何项目的 [00_overview.md](examples/openhands/00_overview.md) 开始看全貌，再逐级深入。

---

## Specs 的结构

Specs 镜像源项目的目录结构：

```
specs-for-project/
├── 00_overview.md          # 项目做什么、技术栈、架构图
├── 01_architecture.md      # 架构决策和理由
├── 02_data_flow.md         # 数据如何在系统中流动
├── _mapping.md             # Spec ↔ 源码文件映射表
├── _glossary.md            # 领域术语表
│
├── src/                    # ← 镜像源码目录
│   ├── core/
│   │   ├── _index.md       # 模块概览 + 导航
│   │   ├── engine.md       # engine.ts 的详细规格
│   │   └── scheduler.md    # scheduler.ts 的详细规格
│   └── api/
│       └── _index.md
```

每个 Spec 文件遵循[标准模板](templates/spec_file.md)，包含 YAML 元数据和固定章节：一句话描述、职责、输入/输出、关键约束、与其他模块的关系、实现笔记。

---

## 双语支持

所有 Skills 支持 `lang` 参数（`en` | `zh`）。模板提供[英文](templates/)和[中文](templates/zh/)两个版本。项目文档也有双语版本。

---

## 与现有工具对比

| 工具 | SpecLens 的不同 |
|------|----------------|
| **DeepWiki** | SpecLens 1:1 镜像源码结构；按需展开细节，而非一次性倾倒所有内容 |
| **Codefetch / Gitingest** | 它们生成扁平的 LLM 友好格式；SpecLens 生成可导航的分层规格 |
| **GitHub Spec Kit** | Spec Kit 是工作流模板；SpecLens 是完整的 Skills 系统，包含 5 个可执行的 Agent 指令 |
| **README / 文档** | 文档是静态的、会腐化的；Specs 是版本化的、可验证的、并驱动代码变更 |

---

## 核心理念

> 代码是实现，Specs 是意图。代码是厕纸，idea 才是关键。

软件开发的历史就是抽象层不断上移：`汇编 → C → Python → Specs`。每一次跃迁，人类都离"机器怎么做"更远，离"我想要什么"更近。

- **Specs 是项目的 API** —— Agent 读 Specs（不是源码）来理解和修改项目
- **Specs 是验收标准** —— 关键约束天然描述测试用例，Agent 可自动派生测试
- **Specs diff 就是人类可读的 changelog** —— Review Spec diff 而非代码 diff

完整理念请阅读：[项目上下文](SpecsDriven_project_context.md)

---

## 项目结构

```
SpecLens/
├── skills/                 # 5 个 Skills（Agent 可执行的指令）
│   ├── analyze/
│   ├── expand/
│   ├── validate/
│   ├── diff-upgrade/
│   └── code-from-spec/
├── templates/              # Spec 文件模板（英文 + 中文）
│   ├── spec_file.md
│   ├── _index.md
│   ├── overview.md
│   ├── architecture.md
│   ├── data_flow.md
│   ├── _mapping.md
│   ├── _glossary.md
│   └── zh/                 # 中文模板
├── examples/               # 真实项目示例 Specs
│   ├── openhands/
│   ├── opencode/
│   ├── claude-code/
│   └── speclens-self/
├── SpecsDriven_project_context.md    # 完整项目上下文（中文）
├── SpecsDriven_project_context_en.md # 完整项目上下文（English）
└── README.md
```

---

## 许可证

MIT
