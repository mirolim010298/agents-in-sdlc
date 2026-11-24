---
title: "第 9 课 - GitHub Copilot CLI 中的斜杠命令"
description: "探索管理上下文、选择模型、分享会话和可选云委派的斜杠命令。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

与其他优秀 CLI 工具一样，GitHub Copilot CLI 提供了许多斜杠命令，用于访问高级功能、查看内部状态和调整配置。你已经使用过 `/diff`、`/mcp`、`/skills`、`/agent` 和 `/pr`。现在探索其他实用命令。

本课将介绍如何使用 `/context` 和 `/compact` 查看对话上下文、使用 `/model` 浏览可用模型、通过 `/share` 导出或分享会话，以及探索并行工作、工作树和云智能体委派等可选命令。

## 场景

核心 CLI 工作流已完成。现在了解上下文管理、切换模型、分享会话，以及可选地将工作委派给 [Copilot 云智能体][about-cloud-agent]。

## 查看 Copilot CLI 上下文

处理大型或复杂任务时，可能会接近模型的上下文窗口限制。Copilot CLI 会在需要时自动压缩对话；你也可以使用斜杠命令查看或手动压缩。

1. 返回 Codespace。如果 Copilot CLI 尚未打开，请从存储库根目录启动。
2. 输入：

   ```plaintext
   /context
   ```

3. 查看模型、当前 token 用量，以及系统说明、工具、消息和剩余空间的上下文分配。
4. 压缩对话：

   ```plaintext
   /compact
   ```

5. 再次输入 `/context` 并比较结果。如果对话本来就较短，变化可能不明显。

> [!NOTE]
> 上下文窗口接近上限时，Copilot CLI 会自动压缩。想自行决定时间时可使用 `/compact`；切换到无关任务并希望开启新对话时，使用 `/clear` 或 `/new`。

## 选择模型

不同模型有不同优势，开发人员也各有偏好。Copilot CLI 可列出并切换模型：

1. 输入：

   ```plaintext
   /model
   ```

2. 浏览可用模型和用量信息。
3. 保留当前模型、选择其他模型，或按 <kbd>Esc</kbd> 关闭列表。

## 分享会话

与团队分享经验有助于提升 AI 工具的使用水平。`/share` 可以将会话导出为 Markdown 或 HTML 文件、创建可分享链接，或发布为 GitHub gist。

1. 输入 `/help`，查看当前版本中的 `/share` 选项。
2. 如果要分享会话，选择合适的目标，例如 `/share file` 导出本地 Markdown 文件。
3. 发送或发布之前先检查导出内容。会话导出可能包含提示、回复和项目细节。

发布链接或 gist 是可选的。不要分享团队不希望公开的存储库或对话内容。

## 可选：扩展并委派工作

核心研讨会已完成。Copilot CLI 还为较大型任务提供以下命令：

- `/fleet`：将独立子任务交给多个子智能体并行执行；
- `/worktree`：为单独任务创建隔离的 Git 工作树；
- `/delegate`：将任务发送给异步工作的 Copilot 云智能体，它可能会创建拉取请求。

这些命令是可选的，因为它们可能创建额外工作树或远程任务。尝试前先创建范围明确的新任务，并按正常流程审查结果。若要深入了解异步智能体，可继续学习[云智能体研讨会][cloud-workshop]。

## 总结和后续步骤

你使用斜杠命令配置 Copilot CLI、分享会话并查看内部状态。你已使用 `/context` 和 `/compact` 查看上下文管理，使用 `/model` 浏览模型，了解了 `/share`，并探索了并行工作、工作树及云智能体委派等可选功能。

还有更多斜杠命令值得探索。接下来[回顾所学内容][next-lesson]并了解后续学习资源。

## 资源

- [Copilot CLI 命令参考][cli-reference]
- [Copilot CLI 中的上下文管理][context-management]
- [关于 Copilot 云智能体][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
