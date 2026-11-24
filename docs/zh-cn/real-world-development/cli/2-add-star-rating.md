---
title: "第 2 课 - 添加星级评分：快速上手"
description: "使用 Copilot CLI 修改游戏卡片，在转发的浏览器中检查更改，并合并第一个拉取请求。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

安装 Copilot CLI 并尝试过对话后，现在来为项目做第一个更改。游戏数据中已有星级评分，但主页的游戏卡片还没有显示它。让智能体展示评分，审查更改并合并第一个拉取请求。

本课将介绍如何：

- 在功能分支中开始聚焦的 Copilot 对话；
- 让智能体进行小幅项目更改；
- 使用 `/diff` 审查更改；
- 启动应用并在转发的浏览器中检查；
- 创建并合并第一个拉取请求。

## 场景

Tailspin Toys 中的每款游戏都可以有星级评分，详情页已经显示评分，但主页卡片只显示标题、类别、发行商和说明。作为热身，请智能体在每张卡片上显示已有评分。

## 对话的组成

**对话**是你使用 Copilot CLI 完成任务的工作区。与 Copilot app 不同，常规 CLI 对话使用终端当前检出的存储库和 Git 分支，不会自动创建专用工作树。保存的对话可以稍后继续，但文件和分支仍是磁盘上的普通 Git 状态。

对话包含三部分：你的提示和智能体回复、智能体探索和编辑文件时的工具活动，以及可通过 `/diff` 检查的更改。

## 开始对话并请求更改

1. 返回 Codespace。
2. 如果终端未打开，按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）。
3. 如果 Copilot CLI 尚未运行，执行：

   ```bash
   copilot --yolo
   ```

4. 输入斜杠命令 `/new` 并按 <kbd>Enter</kbd>，确保开始新会话。
5. 发送以下提示：

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot 会探索项目、查找游戏详情显示逻辑并创建所需代码。现在已使用 Copilot CLI 添加了一个功能。

## 审查差异

合并前应审查所有 AI 生成的更改，即使它们很小：

1. 输入 `/diff` 并检查每个更改文件。
2. 确认游戏卡片在有评分时显示数字评分，在 `starRating` 为 `null` 时显示 `No rating yet`。
3. 确认测试覆盖这两种状态。
4. 查看 Copilot 运行的检查结果，并要求修复任何失败。
5. 审查完成后，按 <kbd>Esc</kbd> 退出差异界面。

> [!NOTE]
> Copilot 和其他生成式 AI 工具具有概率性，因此实际代码可能不同。应审查行为，而不是要求实现完全一致。

## 检查更改

不要只读代码就假定它能正常运行。让 Copilot 启动网站，然后在 Codespaces 转发的浏览器中查看更新后的 UI。

1. 请 Copilot 启动应用：

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces 显示端口 `4321` 可用时，选择 **Open in Browser**。
3. 确认游戏卡片显示满分五分的评分。
4. 返回 Copilot 并发送以下提示，要求停止服务器：

   ```plaintext
   Stop the development server you started.
   ```

## 创建并合并第一个拉取请求

功能已完成，现在创建拉取请求（PR）并将代码合并到项目中。

1. 请默认智能体提交更改：

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. 输入 `/pr create`。Copilot CLI 创建 PR 时会推送现有提交，并显示 PR URL。
3. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），再选择 Copilot CLI 显示的 URL 打开 PR。
4. 审查更改文件和检查结果。
5. 准备就绪后，选择 **Merge pull request** 并确认合并。
6. 返回 Codespace，输入 `/exit` 退出 Copilot CLI。
7. 更新本地 `main`：

   ```bash
   git checkout main
   git pull
   ```

## 总结和后续步骤

恭喜，你已使用 GitHub Copilot CLI 交付第一个更改。你开始了聚焦的 Copilot 对话、指导智能体修改游戏卡片、使用 `/diff` 审查、在转发浏览器中检查星级评分，并创建和合并了第一个 PR。

接下来从筛选议题开始，使用 Plan 和 Autopilot 模式[构建更大的功能][next-lesson]。

## 资源

- [关于 GitHub Copilot CLI][about-copilot-cli]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
