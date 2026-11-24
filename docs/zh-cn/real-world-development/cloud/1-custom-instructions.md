---
title: "练习 1 - 自定义说明（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：准备工作][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，或 Copilot 需要了解背景信息，就要确保它能访问这些上下文。[说明文件][instruction-files]可提供此类指导，帮助 Copilot 理解你不仅希望它做什么，也希望它如何完成。

在本练习中，你将：

- 了解项目上下文、编码指南和文档标准如何通过存储库自定义说明及按路径限定范围的说明文件传递给 Copilot；
- 在 `.github/copilot-instructions.md` 中添加一项新的全库标准。

> [!NOTE]
> 与 VS Code 和 CLI 工作流不同，这里不会运行前后对比提示。Copilot 云智能体会异步处理 GitHub 议题，因此难以实时并排展示说明的影响。稍后审查云智能体创建的拉取请求时，可以看到说明文件发挥的作用。

## 说明文件

### 场景

和优秀的开发团队一样，Tailspin Toys 也有一套开发实践指南和要求，包括：

- 数据层始终需要单元测试。
- UI 应采用深色模式并具有现代感。
- 代码应包含 TSDoc 文档注释。
- 每个文件开头都应有注释块，说明文件用途。

借助说明文件，可以确保 Copilot 掌握正确的信息，并遵循这些实践要求。

### 自定义说明

自定义说明可向 Copilot 提供上下文和偏好，帮助它理解编码风格和需求。你可以指定编码约定、库以及偏好的注释类型。可以为整个存储库创建说明，也可以针对特定文件类型创建说明，为任务提供上下文。

说明文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送此全库说明文件。它应包含适用于大多数 Copilot 聊天或 CLI 请求的项目级信息，例如技术栈、项目概况、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：针对特定任务或文件类型的说明文件。可为 TypeScript 或 Astro 等语言提供指导，也可指导如何创建 UI 组件或一组单元测试。

> [!NOTE]
> 在 IDE 中工作时，说明文件仅用于 Copilot Chat 生成代码，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体生成代码时，都会使用存储库级说明文件以及带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot [还支持其他标准的说明文件][custom-instructions-support]，包括 `AGENTS.md` 和 `CLAUDE.md`。

### 管理说明文件的最佳实践

完整讨论如何创建说明文件超出了本研讨会的范围，但示例项目展示了一种常见做法：

- 将 `copilot-instructions.md` 用于项目级指导，例如项目概况、结构和全局编码标准。
- 使用 `*.instructions.md` 文件为特定文件类型（单元测试、Astro 组件、数据层）或任务提供具体指导。
- 使用自然语言，保持说明清楚，并提供代码应如何编写或不应如何编写的示例。

说明文件没有唯一正确的写法，AI 的使用方式也不止一种。通过尝试，找到适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应具备完善的说明文件。浏览本项目时，可以看到许多任务都有相应文件，例如 [UI 更新][ui-instructions]和 [Astro][astro-instructions]。
>
> Copilot 也可以帮助生成说明文件。不同界面的入口不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。当前工作流的课程会在相关步骤说明入口位置。
>
> 需要模板或起点？可以查看 [awesome-copilot][awesome-copilot]，其中收集了说明文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 浏览本项目的自定义说明文件

花些时间查看此存储库自带的说明文件：一个核心 `copilot-instructions.md`，以及一组面向不同任务的 `*.instructions.md` 文件。可以在编辑器或 GitHub Web UI 中打开。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览文件中的项目简介，以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。注意 **Code standards** 中的 **GitHub Actions Workflows** 子部分。这些说明适用于与 Copilot 的各种交互。
3. 打开 `.github/instructions` 文件夹并浏览，留意针对 Astro 文件、Drizzle 数据层和测试等内容的说明。
4. 打开 `.github/instructions/unit-tests.instructions.md`。查看顶部的 `applyTo` 字段，它设置了相对于存储库根目录的 glob，用于确定说明适用的文件。这里，任何匹配 `**/*.test.ts` 的 TypeScript 测试文件都会匹配。
5. 留意其中为本项目编写单元测试提供的具体说明。
6. 最后打开 `.github/instructions/drizzle.instructions.md` 并滚动到底部。注意它链接到其他说明文件（例如 `unit-tests.instructions.md`）以及项目现有文件。这样可以将较大的说明集拆分成更小、可复用的文件，并为 Copilot 提供可参照的代码示例。此处路径相对于说明文件所在位置，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分记录了项目编码标准，但尚未要求在代码中添加文档。接下来会加入 TSDoc 文档注释和文件注释头规则。

## 添加新的存储库标准

接下来要做的唯一编辑，是添加一条项目级规则，要求在代码中使用 TSDoc 文档注释和文件级注释头。稍后在本工作流中分配议题后，云智能体就会读取这项规则。

编辑前先创建分支。云智能体会从议题目标分支读取说明，但仍应清晰地提交这些编辑：

1. 在 codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在添加存储库编码标准，以改善代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，通常在第 27 行附近。它记录了项目编码标准，但尚未包含代码文档规则，因此生成的 helper 没有文档注释。
3. 在现有标准下方添加以下 Markdown 行，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如上一课所示，可以在存储库级文件（`.github/copilot-instructions.md`）中编写全局指导，也可以用 `*.instructions.md` 文件指导特定语言、文件类型或任务。刚添加的文档注释规则属于项目级标准，应放在存储库级文件中。

## 提交、推送并合并说明更新

云智能体会从议题目标分支读取说明。下一课将从 `main` 分支创建任务，因此必须先将此说明更改合并到 `main`，云智能体才能读取。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 到 `main` 的拉取请求并合并。下一课中分配议题后，云智能体就会读取这些说明。

> [!TIP]
> 如果希望直接在 `main` 上工作，也可以跳过创建分支并直接提交。本练习使用分支是为了模拟真实项目中的工作方式。

## 总结和后续步骤

你已了解 Copilot 如何从项目的说明文件获取上下文，并在 `.github/copilot-instructions.md` 中添加了新的全库标准。后续练习中，云智能体创建的拉取请求将体现这项标准。

接下来，将[第一个议题分配给 Copilot 云智能体][next-lesson]。

## 资源

- [GitHub Copilot 自定义说明文件][instruction-files]
- [创建自定义说明的最佳实践][instructions-best-practices]
- [编写更好 Copilot 自定义说明的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot——说明文件及其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
