---
title: "第 8 课 - 创建并合并功能 PR"
description: "审查筛选功能、说明、技能更新、QA 配置和测试，然后创建 PR 并使用 Agent Merge。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

筛选功能、说明更新、技能更新、质量保证（QA）配置和测试都已保存在同一个分支中。现在一起审查这些更改并创建拉取请求。星级评分 PR 是手动合并的；这次将使用 **Agent Merge** 管理合并流程。

> [!NOTE]
> 实际工作中，通常会把功能、说明、技能和 QA 智能体拆分到几个 PR 中。为简化研讨会，筛选和质量工作都保留在同一个对话与分支中，并通过此 PR 一起交付。

本课将介绍 Agent Merge 如何自动处理合并流程、检查完整功能与验证证据、创建筛选 PR，以及如何在审查后启用 Agent Merge 并确认 PR 已合并。

## 场景

在筛选功能的整个开发流程中，你使用 Copilot 规划、实现并验证了功能。Tailspin Toys 希望自动处理 PR 的后续工作，同时由开发人员掌握合并授权。

## 认识 Agent Merge

**Agent Merge** 会自动处理合并拉取请求所需的剩余工作。启用后，Copilot 会解决阻止 PR 合并的问题，例如修复持续集成 (CI) 检查失败、回应审查意见，以及在需要时变基；如果存储库允许，之后会启用 GitHub 自动合并。

之前由你手动选择 **Merge pull request**。Agent Merge 可以代为处理，但启用前仍应先审查并确认更改已准备就绪。

## 使用 Agent Merge 管理 PR

代码完成后，一起审查代码、创建 PR，并让 Agent Merge 管理后续流程：

1. 返回 Codespace。
2. 输入 `/agent` 打开智能体对话框。
3. 从选项中选择 **Default**，再按 <kbd>Enter</kbd>。
4. 输入 `/pr create` 创建新 PR。
5. 输入 `/pr agentmerge` 启用 Agent Merge。
6. Copilot 会监控 PR 的持续集成。所有检查成功后，它会执行合并。
7. 确认 Copilot 显示类似“PR #14 was squash-merged successfully.”的消息。

> [!IMPORTANT]
> Agent Merge 不会绕过必需审批、分支保护、合并队列、存储库设置或权限要求。如果流程受阻，请查看报告的原因，并在存储库允许时手动完成已审查的合并。

## 总结和后续步骤

你已自动化开发流程中的多个环节，包括生成代码、测试和验证代码，以及处理拉取请求。你了解了 Agent Merge 的工作方式，审查了完整功能和验证证据，创建了筛选 PR，并在审查后启用 Agent Merge 确认 PR 已合并。

接下来[探索更多 Copilot CLI 斜杠命令][next-lesson]，了解上下文、模型、会话分享和可选的云委派。

## 资源

- [使用 Copilot CLI 管理拉取请求][manage-prs]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
