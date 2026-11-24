---
title: "练习 2 - 使用 Copilot 智能体模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是简单的应用更新，通常也需要修改多个文件并运行测试。开发人员需要查找相关文件、进行修改、运行测试、调试并反复修正。Copilot 智能体模式可以在 IDE 中自主探索项目、协调修改、运行任务并修复发现的问题。

> [!NOTE]
> 智能体模式和云智能体名称相似，但适用于不同场景。智能体模式在 IDE 中执行任务，便于快速反馈和交互；云智能体则像团队成员一样异步工作，通过议题和拉取请求与你协作。

本练习将介绍如何使用智能体模式探索项目、跨 UI 和数据层实现功能，以及如何审查生成的更改和测试。

## 场景

游戏列表逐渐变长，需要允许用户按类别和发行商筛选。上一课已添加 publishers helper，现在使用 Copilot 智能体模式完成剩余的数据层、UI 和测试。

## 运行 Tailspin Toys 网站

Tailspin Toys 是一个以开发者为主题的桌游众筹网站。它是一个 Astro 应用，构建时将页面渲染为静态 HTML。页面通过 Drizzle ORM 在 frontmatter 中直接查询本地 SQLite 数据库；没有独立后端 API 或客户端 UI 框架。可复用的数据访问 helper 位于 `src/lib/`，交互功能使用标准 DOM API 编写的小型 Astro `<script>`。

### 启动网站

项目提供 `npm run dev` 命令来启动 Astro 开发服务器：

1. 返回上一课使用的 codespace，确认当前处于 `main`。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
3. 创建筛选功能分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器准备就绪后，会显示类似的 URL：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

5. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），再选择终端中的 `http://localhost:4321`。

> [!NOTE]
> 在 codespace 中选择终端的 localhost 链接时，会自动跳转到 `https://<your-codespace-name>-4321.app.github.dev/`。这是连接到 codespace Web 服务器的私有隧道。

如果 VS Code 提示打开 `http://localhost:4321` 的浏览器窗口，可选择 **x** 关闭提示。

### 浏览网站

网站主要包含首页和游戏详情页：主页列出桌游的标题、图片和说明；选择某款游戏后，会打开显示标题、说明、发行商和类别等信息的详情页。

## 让 Copilot 浏览待办列表

> [!TIP]
> **打开 Copilot Chat**
>
> 返回 codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始干净的新对话。不同练习所需的模式和模型可能不同，按各步骤说明选择。

从模板创建项目时，系统已自动创建议题待办列表。让 GitHub Copilot 展示这些议题：

1. 在 Chat 视图的智能体下拉菜单中选择 **Agent**。Agent 可自主规划并跨文件实现更改、运行终端命令和调用工具。
2. 从模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 选择此模型并不表示作者偏好某个模型。编写研讨会时使用了 Claude Sonnet 4.5，希望让代码建议相对一致。由于 LLM 具有概率性，收到不同建议也属正常。

> [!NOTE]
> Copilot 可能会调用不同的 MCP 命令，但应仍能完成任务。

3. 发送以下提示：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue** 运行列出议题的命令。
5. 查看 Copilot 生成的议题列表和优先级建议。

## 查看说明文件

生成代码前，先查看用于提供上下文的 UI 说明文件：[`.github/instructions/ui.instructions.md`](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)。它说明如何为网站添加功能。

1. 在 codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 查看其中的架构概述、组件设计原则、可测试性与无障碍访问指导，以及指向 Astro、Tailwind CSS 和 Drizzle 说明文件的链接。

> [!TIP]
> 说明文件可以引用其他说明文件和项目文件。路径相对于说明文件所在位置，便于复用内容、拆分复杂指导并提供示例。

## 实现筛选功能

筛选功能至少需要三项更改：

- 在 `src/lib/` 中添加或完善筛选逻辑；
- 添加或更新筛选行为的测试；
- 更新游戏列表页，添加筛选 UI。

Copilot 智能体模式可以完成这些工作：

1. 继续当前对话，或选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions**，再选择 `ui` 说明文件。

   ![选择 UI 说明文件的示例](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图中仍选中 **Agent**。
4. 确认模型仍为 **Claude Sonnet 4.5**。
5. 发送以下提示：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 探索项目并查找相关的数据层、UI 和测试文件，然后修改代码并运行测试。

   ![Copilot 正在探索项目文件](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会探索项目、修改文件并运行测试，过程可能需要几分钟。编辑器中可能出现 **Keep** 和 **Undo** 按钮；无需在工作过程中选择，完成后可以统一审查更改。

7. Copilot 提示运行测试时，选择 **Continue**。
8. 过程中可能会暂停或遇到测试失败，这是正常情况。Copilot 会在生成代码和运行测试之间迭代，直到完成任务且未检测到错误。
9. 检查生成的代码是否存在问题。

   ![Copilot 智能体模式会话完成](../../../_images/ex3-agent-mode-proposed-changes.png)

> [!CAUTION]
> 务必审查 Copilot 或其他 AI 工具生成的代码。

10. 返回正在运行网站的浏览器并试用新功能。
11. 确认功能正常且已审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结和后续步骤

你已了解如何使用 Copilot 智能体模式跨 UI 和数据层实现功能、探索项目并协调更改，以及在合并前审查 Copilot 生成的更改和测试。

接下来使用 [Playwright MCP 服务器测试功能][next-lesson]，并为其创建拉取请求。

### 额外探索练习 — 实现分页

随着游戏列表增长，网站需要分页。使用本练习学到的技能，让 Copilot 添加分页。考虑沿用现有最佳实践和说明文件、决定是否让用户选择每页项目数，以及如何编写提示。可能需要多次迭代并提供上下文，这是正常的协作流程。

## 资源

- [Copilot ask、edit 和 agent 模式：用途及适用场景][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
