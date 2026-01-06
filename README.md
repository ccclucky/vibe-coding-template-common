# Vibe Coding 通用项目模板

本模板基于 [Vibe Coding](https://github.com/EnzeD/vibe-coding) 理念，专为**通用项目开发**（非仅限于游戏）量身定制。它强调**AI 辅助规划**与**人类监督执行**相结合，确保代码库的可维护性和高质量。

## 🌟 核心理念

1.  **规划先行**: 绝对不要让 AI 自主规划。必须由人类（你）发起规划，AI 辅助完善。
2.  **Memory Bank (记忆库)**: 维护一套 AI 可读取的文档（PRD、技术栈、计划、架构），确保 AI 在任何时候都拥有完整的项目上下文。
3.  **小步快跑**: 将任务拆解为微小的、可验证的步骤。每一步必须通过测试才能进入下一步。

## 🚀 快速上手 (Core Flow)

### 第一步：初始化记忆库 (Memory Bank)

在开始写任何代码之前，先填充 `memory-bank` 目录下的核心文档。这些文档是 AI 的"大脑"。

1.  **产品需求 (PRD)**
    *   编辑 `memory-bank/product-requirements-document.md`。
    *   简明扼要地描述你的项目想法、功能需求和目标用户。

2.  **技术选型 (Tech Stack)**
    *   让 AI (如 GPT-5, Claude 3.5 Sonnet) 阅读你的 PRD。
    *   提示词: *"阅读我的 PRD，推荐最简单且稳健的技术栈。"*
    *   将结果保存到 `memory-bank/tech-stack.md`。

3.  **实施计划 (Implementation Plan) —— 最关键的一步**
    *   让 AI 阅读 PRD 和 Tech Stack。
    *   提示词: *"创建一个详细的实施计划。步骤必须非常小且具体。每一步都必须包含验证测试。不要写代码，只写指令。专注于核心 MVP。*
    *   将结果保存到 `memory-bank/implementation-plan.md`。

4.  **查漏补缺 (Making sure everything is clear) —— *非常关键***
    *   在开始写代码前，**必须**让 AI 审查你的计划。
    *   提示词: *"Read all the documents in memory-bank, is implementation-plan.md clear? What are your questions to make it 100% clear for you?"*
    *   AI 通常会问出几个关键问题。回答这些问题，并要求 AI 根据你的回答更新 `implementation-plan.md`。
    *   这一步能极大地减少后续开发中的逻辑错误和返工。

### 第二步：进入 Vibe Coding 循环

设置好 Memory Bank 后，按照以下循环进行开发：

1.  **加载上下文**: 每次开始新对话，确保 AI 读取 `CLAUDE.md` 和 `memory-bank/` 下的所有文件。
2.  **执行单步**:
    *   提示词: *"阅读 memory-bank，执行实施计划的第 X 步。完成后通过 [测试方法] 进行验证。"*
3.  **验证与提交**:
    *   **必须**亲自运行测试或验证功能。
    *   验证通过后，Git Commit 代码。
    *   更新 `memory-bank/progress.md` (记录已完成的步骤)。
    *   更新 `memory-bank/architecture.md` (如果有新文件或架构变更)。
4.  **重置**: 清除 AI 上下文（开启新对话），重复第一步，进行下一个任务。

## 💡 核心技巧

*   **CLAUDE.md**: 项目根目录下的 `CLAUDE.md` 包含项目的"宪法"。确保保留 *"Always read memory-bank/@architecture.md before writing any code"* 等规则，这能防止 AI 产生幻觉或破坏现有架构。
*   **遇到 Bug**:
    *   不要盲目让 AI 试错。
    *   如果你卡住了，使用 `git reset` 回退到上一个稳健的版本，调整提示词重试。
    *   如果报错是具体的，直接把错误信息贴给 AI。
*   **保持进度同步**: `progress.md` 是你和 AI 的同步机制。每次新会话，AI 通过它知道项目进展到哪里了。
