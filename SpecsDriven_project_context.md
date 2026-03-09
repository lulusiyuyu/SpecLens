# SpecLens — Project Context

> 把任何代码库变成人类可理解、Agent 可消费的分层规格文档，让 Specs 成为软件的第一公民。
>
> Specs 是下一层抽象。Agent 是这层抽象的编译器。

---

## 1. 项目是什么

SpecLens 是一套 **Skills / Prompt 模板系统**（非传统软件），以 Markdown 文件的形式存在，可以被任何 AI Coding Agent 加载使用。

它帮助用户完成两件核心事情：

1. **学习理解**：将一个已有的开源项目拆解为从宏观到微观的分层 Specs 文件夹，让人类可以快速理解项目
2. **开发维护**：将 Specs 作为项目的顶层维护单位，通过修改 Specs 来驱动 Agent 修改代码

### 核心理念

> **代码是实现，Spec 才是意图。代码是厕纸，idea 才是关键。**

```
传统开发：  人类 → 代码 → 产品
SpecLens： 人类 → Specs → Agent → 代码 → 产品
```

人类从"写代码的人"变成了"写规格的人"。Specs 就像一门新的更高级的"编程语言"，Agent 就是"编译器"。

### 更深层的视角

软件开发的历史就是抽象层不断上移：`汇编 → C → Python → Specs`。每一次跃迁，人类都离“机器怎么做”更远，离“我想要什么”更近。

- **Specs 不只是文档** —— 它是项目的 API。Agent 不用读源码，只读 Specs 就能理解和修改项目。Spec 的格式设计就是在**定义一种协议**。
- **Specs 不只是描述** —— 它也是验收标准。Spec 中的“关键约束”和“输入/输出”天然就是测试用例的描述，Agent 可以从中自动派生测试。
- **Specs diff 就是人类可读的 changelog** —— PR review 不再看代码 diff，而是看 Specs diff。

模型会越来越强，上下文窗口会越来越大。SpecLens 不是在适配当前模型的局限，而是在为必然到来的未来**提前定义标准**。

---

## 2. 解决什么问题

| 问题 | 当前状态 | SpecLens 如何解决 |
|------|---------|-----------------|
| 学习一个大型开源项目很痛苦 | 读源码、翻文档、看 issue，效率低 | 自动生成分层 Specs，由宏观到微观，按需展开 |
| AI Agent 写代码容易偏离意图 | 缺乏结构化的意图描述 | Specs 作为明确的意图文档指导 Agent |
| 项目文档容易腐化 | 文档和代码分离，更新不同步 | Specs 即文档，且是代码变更的上游源 |
| 想在 AI 过渡期参与调试 | 看代码费劲、看 AI 生成的代码更费劲 | Specs 结构镜像源码结构，人类可快速定位并理解 |

---

## 3. 产品形态

### 形态：Skills / Prompt 模板系统

- **不是** Web 应用、桌面应用、CLI 工具
- **是** 一套结构化的 Markdown 文件（Skills + Templates + Examples）
- 可以加载到任何 AI Coding Agent 中使用（Claude Code、GitHub Copilot、Gemini CLI、Cursor、Windsurf 等）
- 零依赖、零安装、Agent-Agnostic、任何 LLM 可用

### 为什么选这个形态

1. **自洽**：项目理念是"Specs 先行，代码是厕纸"，那项目自身就应该以 Specs/Skills 的形态存在，而不是写一堆代码
2. **最大覆盖面**：不绑定任何 Agent 或 LLM，适配所有平台
3. **零维护成本**：Markdown 没有依赖、没有 runtime、10 年后打开还能用
4. **低门槛**：下载文件夹，丢给 Agent 就能用

---

## 4. 核心功能（以 Skills 实现）

### Skill 1: Analyze — 项目分析与骨架生成

**输入**：一个代码库（本地项目或 GitHub URL）
**输出**：镜像原项目结构的 Specs 文件夹骨架

行为：
- 分析项目的目录结构、技术栈、核心模块
- 生成镜像原项目的 Specs 文件夹结构
- 顶层文件（overview、architecture、data_flow）写入宏观内容
- 内层文件只放骨架（标题 + 一句话描述），**不展开细节**（lazy loading）
- 生成 `_mapping.md`（Spec 文件 ↔ 源码文件的对应表）

### Skill 2: Expand — 按需展开细节

**输入**：指定某个模块/文件的 Spec
**输出**：该模块的详细 Spec 内容

行为：
- 根据用户指定的模块，回到源代码中分析细节
- 填充该模块的职责、输入输出、状态管理、关键约束、与其他模块的关系
- 更新 YAML frontmatter 中的 `status: skeleton → draft`

### Skill 3: Diff & Upgrade — 版本差异与升级

**输入**：修改后的 Specs（或明确的修改意图）
**输出**：代码变更计划 + 执行

行为：
- 对比当前 Specs 与之前版本（通过 Git diff）
- 识别出意图变更
- 生成代码修改任务列表
- （可选）指导 Agent 执行代码修改

### Skill 4: Validate — Specs 一致性检查

**输入**：当前 Specs 文件夹
**输出**：一致性报告

行为：
- 检查 Specs 之间是否有逻辑矛盾
- 检查 Specs 与实际代码是否一致
- 检查是否有模块被遗漏
- 检查依赖关系是否正确

### Skill 5: Code from Spec — 从 Spec 生成代码

**输入**：一个或多个 Spec 文件
**输出**：对应的代码文件

行为：
- 读取 Spec 中的意图、约束、接口定义
- 生成符合 Spec 的代码实现
- 运行测试验证

---

## 5. Specs 文件夹结构设计

### 核心原则

1. **镜像原项目结构**：Specs 的文件夹层级与源代码目录保持一致，方便 Human-in-the-Loop
2. **Lazy Loading 式展开**：外层先生成宏观内容，内层只放骨架占位，用户需要时再展开
3. **每层有 `_index.md`**：作为该层级的导航地图
4. **顶层有全局视角文件**：overview、architecture、data_flow、glossary

### 结构示例

假设原项目结构是：
```
my-project/
├── src/
│   ├── api/
│   │   ├── routes/
│   │   └── middleware/
│   ├── core/
│   │   ├── engine.ts
│   │   └── scheduler.ts
│   ├── models/
│   └── utils/
├── tests/
└── config/
```

对应生成的 Specs：
```
specs-for-my-project/
├── 00_overview.md              # 项目全景：是什么、做什么、架构图
├── 01_architecture.md          # 架构决策、技术选型理由
├── 02_data_flow.md             # 数据在系统中如何流动
├── _mapping.md                 # Spec 文件 ↔ 源代码文件对应表
├── _glossary.md                # 术语表
│
├── src/                        # ← 镜像原项目 src/
│   ├── api/
│   │   ├── _index.md           # API 层概览
│   │   ├── routes/
│   │   │   └── _index.md       # 路由设计（骨架，按需展开）
│   │   └── middleware/
│   │       └── _index.md       # 中间件链说明
│   ├── core/
│   │   ├── _index.md           # 核心模块概览
│   │   ├── engine.md           # 引擎的职责、输入输出、状态机
│   │   └── scheduler.md        # 调度器的策略和约束
│   ├── models/
│   │   └── _index.md           # 数据模型概览 + ER 图
│   └── utils/
│       └── _index.md           # 工具函数聚合说明
│
└── _cross-cutting/             # ← 增加的横切关注点
    ├── error_handling.md
    ├── logging.md
    └── auth.md
```

### 单个 Spec 文件的标准格式

```markdown
---
status: skeleton | draft | reviewed | stable
maps_to: src/core/engine.ts
last_expanded: 2025-03-08
dependencies:
  - src/models/_index.md
  - src/api/_index.md
---

# 模块名称

## 一句话描述
（这个模块做什么，为什么存在）

## 职责
- ...

## 输入/输出
（接收什么、产出什么）

## 关键约束
（性能要求、安全考量、边界条件）

## 与其他模块的关系
（依赖谁、被谁依赖、调用方式）

## 实现笔记
<!-- EXPANDABLE: Agent 按需在此填入技术细节 -->
```

---

## 6. 三种使用模式

### 模式一：学习模式（Reverse Engineering）

```
开源项目 → [Skill: Analyze] → Specs 骨架 → 人类浏览外层
                                             → 感兴趣的模块 → [Skill: Expand] → 深入细节
```

适用场景：学习新技术栈、快速上手新项目、代码审查

### 模式二：开发模式（Forward Engineering）

```
人类想法 → 手写 Specs → [Skill: Code from Spec] → Agent 生成代码
                                                → [Skill: Validate] → 检查一致性
```

适用场景：新项目开发、AI-first 开发流程

### 模式三：维护模式（Iterative Evolution）

```
Specs v1 → 人类修改 Specs → Specs v2
        → [Skill: Diff & Upgrade] → 识别意图变更
        → Agent 修改代码 → 测试 → 上线
```

适用场景：已有项目的迭代升级、需求变更管理

---

## 7. 版本化策略

- **不使用** `specs-v001/`、`specs-v002/` 文件夹
- **使用 Git** 管理 Specs 版本：
  - 每次修改 Specs 后提交 commit
  - 重要版本打 tag（`v0.1.0`、`v0.2.0`）
  - 通过 `git diff` 查看意图变更
  - Git 天然支持 merge、revert、blame、history

---

## 8. Specs 的分类体系

不是所有 Spec 都一样，建议分为五类：

| 类型 | 图标 | 描述 | 示例 |
|------|------|------|------|
| Architecture Spec | 📐 | 系统架构、模块职责、数据流 | `01_architecture.md` |
| Feature Spec | 🎯 | 功能描述、用户故事、验收标准 | `feature_search.md` |
| Interface Spec | 🔧 | API 契约、模块接口定义 | `api/routes/_index.md` |
| Test Spec | 🧪 | 测试策略、边界条件、预期行为 | `_test_strategy.md` |
| Constraint Spec | 📏 | 性能要求、安全要求、兼容性 | `_constraints.md` |

---

## 9. 与现有生态的关系

### 可借鉴/组合的工具

| 工具 | 用途 | 如何组合 |
|------|------|---------|
| **GitHub Spec Kit** | Spec-Driven 开发模板 | 借鉴其四阶段工作流模板设计 |
| **SpecFact CLI** | 代码反向生成 Spec（Python） | 借鉴其 `code2spec` 的分析思路 |
| **DeepWiki / deepwiki-open** | AI 自动生成项目 Wiki | 借鉴其架构图自动生成和层级文档结构 |
| **Codefetch / Gitingest** | 代码库 → LLM 友好格式 | 可作为 Analyze Skill 的前置步骤 |
| **AGENTS.md** | AI Agent 上下文标准 | 借鉴其给 Agent 的指令格式 |

### SpecLens 的独特价值（现有工具不做的）

1. **镜像原项目结构** — 不是抽象的功能分组，而是和代码目录 1:1 对应
2. **Lazy Loading 式展开** — 不一次性生成全部细节，骨架先行、按需深入
3. **三模式统一** — 学习、开发、维护共用一套 Specs 基础设施
4. **Human-in-the-Loop 友好** — 专为过渡期人类参与调试优化
5. **纯 Skills 形态** — 零依赖、Agent-Agnostic、任何 LLM 可用
6. **Specs 即项目 API** — Agent 消费 Specs 而非源码来理解和修改项目
7. **Specs 即验收标准** — 约束描述可自动派生测试，闭环意图→实现→验证

---

## 10. 设计原则

1. **Specs 是第一公民**：一切从 Specs 出发，代码只是 Specs 的产物
2. **人类可读优先**：Specs 中使用人类好理解的语言，而非技术术语堆砌
3. **按需展开**：不做信息过载的全量生成，尊重用户的注意力
4. **结构即导航**：文件夹结构本身就是一张地图，不需要额外的索引系统
5. **Agent-Agnostic**：不绑定任何 AI 平台或 LLM，任何 Agent 都能用
6. **版本化友好**：与 Git 天然兼容，支持 diff/merge/history
7. **自洽**：项目自身就以 Specs/Skills 形态存在，践行自己的理念

---

## 11. 关键设计备忘

- **Specs 粒度**：描述 What 和 Why，不描述 How。太细就变成了代码，失去抽象价值。
- **单向依赖**：永远从 Specs → 代码。Validate Skill 保证一致性。
- **模型会进步**：当前的上下文窗口限制、跨 Agent 一致性问题，随着模型进步都会自然解决。SpecLens 不需要为这些设计 workaround，专注定义好格式标准即可。

---

## 12. 项目路线图

详细的可执行任务列表见 [TODOLIST.md](./TODOLIST.md)。

**总体节奏**：
1. 打磨 Analyze + Expand Skill → 用真实项目跑通
2. Dogfooding：用 SpecLens 分析 SpecLens 自身
3. 用 SpecLens 分析目标项目（OpenHands、OpenCode、claude-code），建立示例 Gallery
4. 补全剩余 Skills（Validate、Diff & Upgrade、Code from Spec）
5. 编写 README + 开源发布

---

## 13. Quick Reference

| 属性 | 值 |
|------|---|
| **项目名称** | SpecLens（暂定，可更换） |
| **产品形态** | Skills / Prompt 模板系统（Markdown 文件夹） |
| **核心理念** | Specs 先行，代码是 Specs 的产物；Specs 是下一层抽象，Agent 是编译器 |
| **核心功能** | Analyze → Expand → Validate → Diff/Upgrade → Code from Spec |
| **目标用户** | 使用 AI Agent 进行开发/学习的开发者 |
| **技术依赖** | 无（纯 Markdown，Agent-Agnostic） |
| **版本管理** | Git（分支 + 标签） |
| **灵感来源** | Twitter Specs-Driven 开发实践分享 |
| **竞品/参考** | GitHub Spec Kit、SpecFact、DeepWiki |
| **目标示例项目** | OpenHands、OpenCode、claude-code |
