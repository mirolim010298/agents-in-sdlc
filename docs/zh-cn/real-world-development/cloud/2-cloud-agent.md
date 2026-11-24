---
title: "练习 2 - GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：自定义说明][previous-lesson]

许多组织都面临技术债务，例如尚未解决的安全问题、需要更新的旧代码，或长期搁置的功能请求。GitHub Copilot 云智能体可自主执行更新代码、添加功能等任务。工作完成后，它会创建草稿拉取请求，供开发人员审查。这样可以将繁琐任务交给智能体处理，让开发人员专注于更重要的工作。

本课将介绍：

- 如何自定义代码生成环境；
- 如何确保操作安全；
- 清晰界定议题范围的重要性；
- 如何将议题分配给 Copilot。

## 场景

Tailspin Toys 有一些技术债务需要处理。最初创建网站的承包商没有为项目编写文档。团队希望先为应用程序中所有导出的函数添加 TSDoc 文档注释。

此外，设计团队希望改进游戏发现体验：在每款游戏的详情页展示同一类别中的其他游戏，方便用户继续浏览。团队暂时只需要可用于验收测试的初步实现。这类任务经常被更高优先级的工作挤到待办列表末尾，正适合交给云智能体异步处理。

## 认识 GitHub Copilot 云智能体

[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent)可以像开发人员一样在后台处理任务。你可以通过多种方式启动任务，例如[将 GitHub 议题分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配后，Copilot 会创建草稿拉取请求来跟踪进度、设置环境并开始工作。你可以在会话运行期间或完成后查看详情。解决方案准备好供审查时，Copilot 会在拉取请求中通知你。

## 清晰界定任务范围的重要性

GitHub Copilot 没有魔法，使用它并不能省去思考。即使看似简单的操作，也可能包含复杂细节，因此请参考[云智能体最佳实践][cloud-agent-best-practices]，明确任务范围。把它当作 AI 结对编程伙伴：分阶段工作、学习、尝试并不断调整。加入生成式 AI 并不会改变软件开发的基本原则。

## 本存储库中的自定义说明

之前的练习介绍了自定义说明及其作用。如果你已完成相关练习，就会看到 `.github/copilot-instructions.md` 的实际效果；否则，现在可以快速查看。分配任务前，先只读浏览存储库中的说明文件，之后便能识别它们对智能体工作的影响：

- `.github/copilot-instructions.md`：查看 **Code standards** 部分，尤其是 TypeScript 约定和 TSDoc 文档注释要求。
- `.github/instructions/unit-tests.instructions.md`：留意 `applyTo` frontmatter，它将说明限定到 `**/*.test.ts` 文件。

下一节将 `Code lacks documentation` 议题分配给云智能体时，检查拉取请求是否遵循了 TSDoc、TypeScript 约定和文件注释头；后续练习会再次检查这些内容。

## 为云智能体设置开发环境

无论由谁编写代码，通常都需要特定环境和设置脚本。将任务分配给 Copilot 时也是如此，因为它会以类似软件工程师的方式工作。

云智能体使用 [GitHub Actions][github-actions] 执行任务。可以在 `.github/workflows/copilot-setup-steps.yml` 中配置[专用设置工作流][setup-workflow]，在工作开始前安装所需工具和依赖项。本实验已提前配置该工作流，其中包含 Node.js、项目依赖项、端到端测试所需的浏览器，以及已迁移并填充数据的 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# Allows you to test the setup steps from your repository's "Actions" tab
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Set the permissions to the lowest permissions possible needed for *your steps*. Copilot will be given its own token for its operations.
    permissions:
      # If you want to clone the repository as part of your setup steps, for example to install dependencies, you'll need the `contents: read` permission. If you don't clone the repository in your setup steps, Copilot will do this for you automatically after the steps complete.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Frontend / app setup - Node.js (the whole app is now Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migrate + seed the local SQLite database so builds and tests have data.
      - name: Set up the database
        run: npm run db:setup
```

此文件与其他 GitHub 工作流类似，但有两点值得留意：

- 它只有一个名为 `copilot-setup-steps` 的作业，会在 Copilot 开始处理拉取请求前于 GitHub Actions 中运行。
- `workflow_dispatch` 触发器可让你在存储库的 **Actions** 选项卡中手动运行工作流，以便测试，而不必等待 Copilot 启动它。

## 添加文档

许多项目的文档过时或缺失，这类技术债务会降低效率，也会增加维护代码库或帮助新成员上手的难度。Copilot 擅长生成文档，因此可以把此任务分配给云智能体，并稍后审查结果。

1. 在新浏览器选项卡中打开 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题窗口。
4. 选择 **Blank issue**。
5. 将 **Title** 设置为 `Code lacks documentation`。
6. 将 **Description** 设置为：

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配窗口。

  ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。
10. 选择 **Pull Requests** 选项卡。
11. 打开新生成的拉取请求（PR），标题可能类似于 `[WIP]: Code lacks documentation`。如果列表中暂时没有 PR，请稍等片刻并刷新页面。
12. 几分钟后，Copilot 应会创建待办列表。

> [!NOTE]
> 待办列表可能需要几分钟才会出现在 PR 中。Copilot 正在创建环境（运行前面介绍的工作流）、分析项目并确定解决问题的最佳方法。

13. 查看 Copilot 将要执行的任务。
14. 向下滚动 PR 时间线，确认 Copilot 已开始处理议题。
15. 选择 **View session**。

  ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 可能需要刷新页面才能看到更新后的状态。

16. 浏览实时会话，观察 Copilot 如何探索代码、了解现状、制定计划并编写代码。

这可能需要几分钟。云智能体的主要优势之一是可以异步执行任务，让你继续处理其他工作。现在再分配一项任务，然后转而为应用添加功能。

## 为游戏详情页添加相关游戏

云智能体可以让你把工作拆分开来：你处理一组任务，它同时处理另一组。现在将设计团队的相关游戏功能分配给云智能体：

1. 返回 github.com 上的存储库。
2. 选择 **Issues** 选项卡，再选择 **New issue**。
3. 选择 **Blank issue**。
4. 将 **Title** 设置为 `Show related games on the game details page`。
5. 将 **Description** 设置为：

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

6. 选择 **Create** 创建议题。
7. 在右侧选择 **Assign to Copilot**，再选择 **Assign**。

议题的第一条评论中很快会出现 👀，表示 Copilot 已开始处理。云智能体会像软件工程师一样工作；无需持续监控，等工作完成后再审查即可。接下来学习创建和使用自定义智能体。

## 总结和后续步骤

本课介绍了 [GitHub Copilot 云智能体][copilot-agents]。可以将议题分配给 Copilot，让它异步处理技术债务、新功能或框架迁移任务。

你已了解如何自定义代码生成环境、确保操作安全、清晰界定议题范围，以及将议题分配给 Copilot。

云智能体继续在后台工作时，可以开始创建和使用自定义智能体。[云智能体也支持 MCP 服务器][cloud-agent-mcp]，并可使用之前练习中设置的自定义说明。

## 资源

- [关于 Copilot 云智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
