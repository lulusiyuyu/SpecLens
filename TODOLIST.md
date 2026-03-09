# SpecLens — TODOLIST

> 本文件是项目的完整可执行任务列表。配合 `SpecsDriven_project_context.md` 阅读，足以指导 Agent 完成整个项目。
>
> **原则：做一个完美的示例，胜过做一百个功能。**

---

## Phase 0: 项目结构初始化

- [x] **0.1** 创建项目目录结构：
  ```
  SpecLens/
  ├── skills/              # 所有 Skill 文件
  │   ├── analyze/
  │   │   └── SKILL.md
  │   ├── expand/
  │   │   └── SKILL.md
  │   ├── validate/
  │   │   └── SKILL.md
  │   ├── diff-upgrade/
  │   │   └── SKILL.md
  │   └── code-from-spec/
  │       └── SKILL.md
  ├── templates/           # Spec 文件模板
  │   ├── spec_file.md     # 单个 Spec 文件的标准模板
  │   ├── _index.md        # 每层目录的导航模板
  │   ├── overview.md      # 顶层 overview 模板
  │   ├── architecture.md  # 顶层 architecture 模板
  │   ├── data_flow.md     # 顶层 data_flow 模板
  │   ├── _mapping.md      # Spec ↔ 源码映射表模板
  │   └── _glossary.md     # 术语表模板
  ├── examples/            # 示例 Specs（用真实项目生成）
  │   ├── speclens-self/   # SpecLens 自身的 Specs（Dogfooding）
  │   ├── openhands/       # OpenHands 的 Specs
  │   ├── opencode/        # OpenCode 的 Specs
  │   └── claude-code/     # claude-code 的 Specs
  ├── SpecsDriven_project_context.md
  ├── TODOLIST.md
  └── README.md
  ```
- [x] **0.2** 初始化 Git 仓库，创建 `.gitignore`
- [x] **0.3** 创建初始 README.md（简洁版，后续 Phase 4 完善）

---

## Phase 1: 核心模板 + 核心 Skills

> 目标：让 Analyze 和 Expand 两个 Skill 可以端到端跑通。

### 1A: 设计模板

- [x] **1A.1** 编写 `templates/spec_file.md` — 单个 Spec 文件的标准格式
  - YAML frontmatter：status、maps_to、last_expanded、dependencies
  - Markdown body：一句话描述、职责、输入/输出、关键约束、与其他模块的关系、实现笔记
  - 参考 `SpecsDriven_project_context.md` 第 5 节的格式设计
- [x] **1A.2** 编写 `templates/_index.md` — 每层目录的导航模板
  - 该层的模块列表 + 一句话描述
  - 模块间关系的简要说明
- [x] **1A.3** 编写顶层模板（overview / architecture / data_flow / _mapping / _glossary）
  - overview：项目是什么、做什么、技术栈、架构图（Mermaid）
  - architecture：架构决策、技术选型理由、核心模块关系
  - data_flow：数据如何在系统中流动（端到端路径描述）
  - _mapping：Spec 文件 ↔ 源码文件的对应表
  - _glossary：项目中的领域术语解释

### 1B: 编写 Analyze Skill

- [x] **1B.1** 编写 `skills/analyze/SKILL.md`
  - 输入：代码库路径（本地项目）
  - 输出：镜像原项目结构的 Specs 文件夹
  - Skill 指令需明确以下步骤：
    1. 读取项目根目录结构 + README + 入口文件
    2. 识别技术栈、核心模块、项目类型
    3. 生成镜像目录结构的 Specs 文件夹
    4. 填写顶层文件（overview / architecture / data_flow）内容
    5. 为每个子目录生成 `_index.md`（含一句话描述）
    6. 为关键源码文件生成骨架 Spec（标题 + 一句话，status: skeleton）
    7. 生成 `_mapping.md` 和 `_glossary.md`
  - Skill 中要包含使用模板的明确引用路径

### 1C: 编写 Expand Skill

- [x] **1C.1** 编写 `skills/expand/SKILL.md`
  - 输入：指定的 Spec 文件路径
  - 输出：该 Spec 的详细内容
  - Skill 指令需明确以下步骤：
    1. 读取指定的骨架 Spec 文件
    2. 根据 `maps_to` 找到对应源码文件
    3. 深入分析源码：职责、接口、状态管理、关键逻辑
    4. 按 spec_file 模板填充所有 section
    5. 更新 status: skeleton → draft
    6. 更新 last_expanded 时间戳

---

## Phase 2: Dogfooding + 真实项目验证

> 目标：用 SpecLens 分析真实项目，验证并迭代 Skill 质量。

### 2A: Dogfooding

- [x] **2A.1** 用 Analyze Skill 分析 SpecLens 项目自身 → 生成 `examples/speclens-self/`
- [x] **2A.2** 审查生成结果，记录需要调整 Skill 的地方
- [x] **2A.3** 迭代修改 Analyze Skill，重新生成，直到满意

### 2B: 目标项目 — OpenHands

- [x] **2B.1** Clone OpenHands 项目到本地
  - `git clone https://github.com/All-Hands-AI/OpenHands`
- [x] **2B.2** 用 Analyze Skill 生成 `examples/openhands/` 的 Specs 骨架
- [x] **2B.3** 用 Expand Skill 展开 3-5 个核心模块的 Spec
- [x] **2B.4** 审查结果，迭代 Skill

### 2C: 目标项目 — OpenCode

- [x] **2C.1** Clone OpenCode 项目到本地
  - `git clone https://github.com/opencode-ai/opencode`
- [x] **2C.2** 用 Analyze Skill 生成 `examples/opencode/` 的 Specs 骨架
- [x] **2C.3** 用 Expand Skill 展开 3-5 个核心模块的 Spec
- [x] **2C.4** 审查结果，迭代 Skill

### 2D: 目标项目 — claude-code

- [x] **2D.1** Clone claude-code 项目到本地
  - `git clone https://github.com/anthropics/claude-code`
- [x] **2D.2** 用 Analyze Skill 生成 `examples/claude-code/` 的 Specs 骨架
- [x] **2D.3** 用 Expand Skill 展开 3-5 个核心模块的 Spec
- [x] **2D.4** 审查结果，迭代 Skill

---

## Phase 3: 补全剩余 Skills

> 目标：完成全部 5 个 Skill，覆盖学习、开发、维护三种模式。

- [x] **3.1** 编写 `skills/validate/SKILL.md` — Specs 一致性检查
  - 检查 Specs 之间的逻辑一致性
  - 检查 Specs 与实际代码是否对应
  - 检查是否有模块被遗漏
  - 输出一致性报告

- [x] **3.2** 编写 `skills/diff-upgrade/SKILL.md` — 版本差异与升级
  - 对比当前 Specs 与之前版本（通过 Git diff）
  - 识别意图变更，生成人类可读的变更摘要
  - 生成代码修改任务列表
  - 可选：指导 Agent 执行代码修改

- [x] **3.3** 编写 `skills/code-from-spec/SKILL.md` — 从 Spec 生成代码
  - 读取 Spec 中的意图、约束、接口定义
  - 从约束描述中自动派生测试用例
  - 生成符合 Spec 的代码实现
  - 运行测试验证

---

## Phase 3.5: 中英文双语适配

> 目标：所有 Skills、模板、示例、文档均支持中英文，面向国际社区。

### 3.5A: Skill 文件双语化

- [x] **3.5A.1** 为每个 Skill 添加 `lang` 参数支持（在 SKILL.md 的指令中）
  - Skill 接受 `lang: zh | en` 参数，控制生成的 Specs 使用中文还是英文
  - 默认 `lang: en`（面向国际社区）
  - Skill 文件本身用英文编写（作为国际标准），关键术语附中文注释
- [x] **3.5A.2** 在每个 Skill 指令中添加语言相关的明确规则：
  - section 标题的中英文对照（如 `## Responsibilities` / `## 职责`）
  - 用人类自然语言描述，不能中英混杂（要么全中文，要么全英文）
  - 术语表 `_glossary.md` 中同时保留中英文术语

### 3.5B: 模板文件双语化

- [x] **3.5B.1** 采用双版本方案：英文模板保留在 `templates/` 根目录（默认），中文模板放在 `templates/zh/`
- [x] **3.5B.2** 创建 `templates/zh/` 目录，包含全部 7 个中文模板文件

### 3.5C: 英文版端到端测试

- [x] **3.5C.1** 英文版 Specs 已在 Phase 2B 生成（`examples/openhands/`），用词自然、结构完整
- [x] **3.5C.2** 英文版 Specs 已在 Phase 2C 生成（`examples/opencode/`），质量达标
- [x] **3.5C.3** 英文版 Specs 已在 Phase 2D 生成（`examples/claude-code/`），质量达标
- [x] **3.5C.4** 确认：三个项目英文 Specs 结构一致、信息量完整、术语表覆盖充分

### 3.5D: 项目文档双语化

- [x] **3.5D.1** `SpecsDriven_project_context.md` 编写对应英文版 `SpecsDriven_project_context_en.md`
- [x] **3.5D.2** `TODOLIST.md` 编写对应英文版 `TODOLIST_en.md`

---

## Phase 4: README + 开源发布

> 目标：写一个让人一看就想用的 README，中英文双语，然后发布。

- [x] **4.1** 编写完整版 `README.md`（英文，作为仓库主 README），包含：
  - 一句话介绍
  - 核心理念（Specs is the next abstraction layer; Agent is the compiler）
  - 30 秒 Quick Start（3 步：download → feed to Agent → see results）
  - 链接到一个示例项目的 Specs（如 `examples/openhands/`）
  - 三种使用模式说明（Learn / Build / Maintain）
  - Skill 列表 + 简要说明
  - 与现有工具的对比
  - 顶部添加 `[中文](./README_zh.md)` 切换链接

- [x] **4.2** 编写 `README_zh.md`（中文版 README）
  - 内容与英文版对等
  - 顶部添加 `[English](./README.md)` 切换链接

<!-- 我已经在wsl里面配置了gh cli 还有就是，我的用户名是lulusiyuyu -->

- [x] **4.3** 在 GitHub 创建仓库并推送
- [x] **4.4** 在两版 README 中添加示例项目 Specs 的链接

---

## 完成标准

整个项目在以下条件满足时视为完成：

1. **5 个 Skill 文件**都已编写且指令清晰、Agent 可执行
2. **模板文件**齐全且格式统一
3. **至少 3 个真实项目的示例 Specs** 存在于 `examples/` 中
4. **中英文双语**：Skills 支持 `lang` 参数、README 有中英双版本、至少 1 个示例项目有英文版 Specs
5. **README** 清晰到任何人 3 分钟内就能理解项目并开始使用
6. 项目自身被 SpecLens 分析过（Dogfooding 完成）

