---
title: "练习 1 - 自定义说明（VS Code）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：准备工作][previous-lesson] · [下一课：智能体模式 →][next-lesson]

使用生成式 AI 时，上下文至关重要。任务可能需要遵循特定方式，或依赖 Copilot 应了解的背景信息。[说明文件][instruction-files]可以提供这些指导。

在本练习中，你将：

- 了解项目上下文、编码指南和文档标准如何通过存储库级和路径级说明传给 Copilot；
- 在当前说明下生成筛选功能的第一块数据切片（publishers helper）；
- 在 `.github/copilot-instructions.md` 中添加全库标准；
- 重新运行相同提示，观察生成代码如何应用新标准；
- 将说明更新和筛选功能基础提交到 `main`，供下一课使用。

> [!CAUTION]
> 生成的代码可能不会完全遵循设定的标准。Copilot 具有非确定性。本练习的重点是观察更新说明后行为的整体变化，而不是要求输出逐字符一致。

## 说明文件

### 场景

Tailspin Toys 的开发实践要求包括：

- 数据层始终需要单元测试；
- UI 应采用深色模式并具有现代感；
- 代码应包含 TSDoc 文档注释；
- 每个文件开头都应添加说明文件用途的注释块。

使用说明文件可确保 Copilot 知道这些要求并据此工作。

### 自定义说明

自定义说明可为 Copilot 提供上下文和偏好，帮助它了解编码风格和需求。可以指定编码约定、库和偏好的注释类型。说明既可用于整个存储库，也可针对特定文件类型。

说明文件分为两类：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送此文件。它应包含项目级信息，例如技术栈、项目概况、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：用于特定任务或文件类型，可指导 TypeScript、Astro、UI 组件或单元测试等工作。

> [!NOTE]
> 在 IDE 中，说明文件仅用于 Copilot Chat 生成代码，不会影响代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体生成代码时，都会使用存储库级说明文件以及带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot [还支持其他标准的说明文件][custom-instructions-support]，包括 `AGENTS.md` 和 `CLAUDE.md`。

### 管理说明文件的最佳实践

- 将 `copilot-instructions.md` 用于项目说明、项目结构和全局编码标准。
- 使用 `*.instructions.md` 为特定文件类型（如单元测试、Astro 组件、数据层）或任务提供具体说明。
- 使用清楚的自然语言，并提供代码应该或不应该如何编写的示例。

说明文件的写法没有唯一标准。通过尝试找到适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应具备完善的说明文件。本项目提供了许多任务的说明，例如 [UI 更新][ui-instructions]和 [Astro][astro-instructions]。
>
> Copilot 也可以帮助生成说明文件，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。也可以从 [awesome-copilot][awesome-copilot] 获取模板和示例。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 浏览本项目中的自定义说明文件

项目附带一个核心 `copilot-instructions.md` 和一组面向不同任务的 `*.instructions.md` 文件。可以在编辑器或 GitHub Web UI 中查看。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览项目简介、**Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。注意 **Code standards** 下的 **GitHub Actions Workflows** 指导。
3. 打开 `.github/instructions` 文件夹，查看针对 Astro、Drizzle 数据层和测试等内容的说明。
4. 打开 `.github/instructions/unit-tests.instructions.md`。顶部的 `applyTo` 字段设置了相对于存储库根目录的 glob；匹配 `**/*.test.ts` 的 TypeScript 测试文件会应用这些说明。
5. 浏览其中为本项目编写单元测试提供的具体指导。
6. 打开 `.github/instructions/drizzle.instructions.md` 并滚动到底部，查看它对其他说明文件和项目现有文件的引用。这种方式可以拆分较大的说明集并提供示例。路径相对于说明文件所在位置，而不是存储库根目录。

> [!NOTE]
> `.github/copilot-instructions.md` 的 **Code formatting requirements** 部分尚未要求在代码中添加文档。接下来会加入 TSDoc 文档注释和文件注释头规则。

## 为更改创建分支

1. 返回上一课使用的 codespace。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
3. 创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions
   ```

## 更新说明前使用 Copilot Chat

> [!TIP]
> **打开 Copilot Chat**
>
> 返回 codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。不同练习使用的模式和模型可能不同；每个步骤会说明相关选择。

先在当前说明下发送提示，观察自定义说明的影响。稍后更新说明并重新发送相同提示。

1. 关闭之前练习留下的编辑器标签页，避免 Copilot 获取不需要的上下文。
2. 打开 `src/lib/publishers.ts`，让 Copilot 知道 helper 应放置的位置。
3. 在 Chat 视图的智能体下拉列表中选择 **Agent**，以便 Copilot 修改文件。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

4. 发送以下提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot 会探索项目并应用代码更改，通常还会更新测试。
6. 查看生成的 helper：它应是一个带类型的函数，第一个参数接收 `db` 客户端，并返回带类型的 publishers 数组。这来自 `.github/instructions/drizzle.instructions.md` 的数据层约定，该文件适用于 `src/lib/*.ts`。
7. 注意生成的代码**缺少** TSDoc 文档注释和文件级注释头。

> [!CAUTION]
> Copilot 具有非确定性，即使没有明确要求，也可能添加文档注释。如果遇到这种情况也没关系；本练习仍要观察更新说明后行为是否更加一致。

## 添加新的存储库标准

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分（通常在第 27 行附近）。它记录了项目编码标准，但尚未包含代码文档规则。
3. 在现有标准下方添加以下 Markdown 行：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 存储库级说明文件适合放置全局标准；`*.instructions.md` 文件则适用于特定语言、文件类型或任务。刚添加的文档注释规则属于项目级标准。

## 重新运行提示并观察变化

1. 返回 Copilot Chat，选择 **New Chat** 开始新对话。
2. 重新打开 `src/lib/publishers.ts`，让 Copilot 聚焦正确文件。
3. 再次发送相同提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 查看文件开头新增的注释块，例如：

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 查看函数新增的 TSDoc 注释，例如：

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

你已引导 Copilot 遵循新的项目标准，并将其应用到真实代码中。下一课会继续扩展这些代码。

## 提交说明并推送分支

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
2. 运行以下命令，确认说明更新和 helper 更改已存在：

   ```bash
   git status
   ```

3. 暂存并提交说明更新及 helper 基础。如果 `git status` 显示 Copilot 还修改了其他文件（例如测试），也要一并暂存：

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # If git status shows additional supporting updates (for example tests), add those files too.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 推送分支：

   ```bash
   git push -u origin custom-instructions
   ```

## 创建并合并拉取请求

分支推送后，需要创建拉取请求并关联待办列表中的文档标准议题。Copilot 可以使用已连接到项目的 GitHub 工具来查找议题、创建关联 PR 并合并。

> [!NOTE]
> 这是第一次让 Copilot 代表你在 GitHub 上操作。项目模板已配置 GitHub 工具，无需额外设置。Copilot 首次使用时，VS Code 可能会提示你登录 GitHub，请按照提示完成授权。后续练习会介绍这种连接所用的 Model Context Protocol。

1. 在 codespace 中打开 Copilot Chat。
2. 按 <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd>（Windows/Linux）打开 Copilot Chat 视图，并确保智能体选择器中已选中 **Agent**。
3. 请 Copilot 查找与更新说明文件相关的议题，并从当前分支创建 PR，说明该 PR 会关闭此议题，同时包含 publishers helper 基础：

   ```text
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot 会查找议题并创建 PR。出现授权提示时，先检查操作，再选择 **Allow**。
5. PR 创建后，发送以下提示，要求 Copilot 合并 PR 并将本地分支切回 `main`：

   ```text
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

6. 出现 GitHub 操作或 shell 命令授权提示时，检查操作后再选择 **Allow**。

你已借助 GitHub Copilot 创建并合并拉取请求。

## 总结和后续步骤

你了解了 Copilot 如何从项目说明文件中获取上下文，并在 VS Code 的 Copilot Chat 中：

- 发送代码生成提示，观察现有说明下的输出；
- 在 `.github/copilot-instructions.md` 中添加全库标准；
- 重新运行提示，观察生成代码如何遵循新标准；
- 将说明更新和 helper 基础提交到 `main`，供下一课继续使用。

接下来使用[智能体模式][next-lesson]，让 Copilot 跨代码库添加新功能。

## 资源

- [GitHub Copilot 自定义说明文件][instruction-files]
- [创建自定义说明的最佳实践][instructions-best-practices]
- [编写更好 Copilot 自定义说明的 5 个技巧][copilot-instructions-five-tips]
- [GitHub Copilot 个人自定义说明][personal-instructions]
- [Awesome Copilot——说明文件及其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
