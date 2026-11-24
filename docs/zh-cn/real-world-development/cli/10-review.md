---
title: "第 10 课 - 总结和后续步骤"
description: "回顾 Copilot CLI 工作流、两个拉取请求、可复用自定义项和后续资源。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

你在 Tailspin Toys 的连续工作流中使用了 GitHub Copilot CLI。你已：

- 准备 Codespace、安装 Copilot CLI、探索项目并找到预置的筛选议题；
- 添加星级评分，在转发浏览器中检查结果，并手动合并第一个拉取请求（PR）；
- 从筛选议题开始，在 Plan 模式定义方案，在 Autopilot 模式构建功能，并在 Interactive 模式审查；
- 使用自定义说明指导智能体，调整 `quality-checks` 技能并运行单元测试、lint 和类型检查；
- 添加 Playwright Model Context Protocol (MCP) 服务器，并在真实浏览器中检查筛选行为；
- 创建并选择质量保证（QA）自定义智能体，评估需求、覆盖率、技能结果和浏览器证据；
- 审查完整筛选更改，并授权 Agent Merge 合并筛选 PR；
- 探索用于上下文、模型、分享和可选云委派的斜杠命令。

## 交付的内容

本研讨会包含两个 PR 阶段，每个都从更新后的 `main` 创建独立分支：

1. **星级评分：**在游戏卡片中显示现有的 `starRating` 和明确的未评分状态。
2. **筛选和质量工作流：**实现筛选、更新并应用说明、自定义 `quality-checks` 报告、创建 QA 配置，并加入相关测试。

从规划筛选功能到创建其 PR，你一直使用同一个对话和分支。为了简化研讨会，这些更改被汇总到一个 PR 中。

## 不同类型的验证

你通过多种方式检查代码：自动化测试、亲自在浏览器中查看，以及使用 MCP 让 Copilot 在浏览器中探索。`quality-checks` 技能运行单元测试、lint 和类型检查，并按新格式报告结果。QA 综合检查结果、需求和测试覆盖率后再审查 PR。

新增测试应解决实际覆盖缺口；如果 QA 检查后无需添加测试，也可能是合理结果。合并前审查代码和证据；代码更改后应重新生成受影响的验证证据。

## 最佳实践

提供给 Copilot 的上下文和工具会影响工作结果。本研讨会中，你更新了说明、自定义了技能、创建了 QA 配置并设置 MCP 服务器。可以在多个对话中复用这些自定义项，并根据团队需求调整。说明定义标准，技能描述可重复任务，自定义智能体定义专用角色，MCP 服务器连接外部工具。应审查实际更改和工具结果，而不只看智能体摘要。

根据任务选择**模式和模型**：使用 **Plan** 先讨论方案，使用 **Interactive** 处理需要密切协作的更改，使用 **Autopilot** 执行范围明确的任务。常规编辑可选择更快的模型，复杂工作则选择能力更强的模型。

上下文和基础设施同样重要。清楚说明要构建什么、为什么构建以及如何实现，会显著影响输出。

## 继续探索

核心工作流已完成。还可以试试以下 Copilot CLI 功能：

- `/review`：请代码审查智能体分析更改；
- `/rubber-duck`：讨论问题并获得另一种观点；
- `/fleet`：并行协调独立子任务；
- `/worktree`：隔离单独任务；
- `/delegate`：将任务发送给 Copilot 云智能体。

## 后续步骤

熟练使用工具的最佳方式就是持续实践。可以将它用于生产代码、个人项目，或一直想做却尚未开始的小应用。与团队分享经验并相互学习，同时继续探索文档。

如果想继续从终端扩展 Tailspin Toys，可以学习可选的 [Foundry Backer Concierge 系列][foundry]。也可以探索 [VS Code 研讨会][vscode]、[GitHub Copilot app 研讨会][app]或 [Copilot 云智能体研讨会][cloud]。

## 资源

- [关于 GitHub Copilot CLI][about-cli]
- [Copilot CLI 命令参考][cli-reference]
- [自定义 Copilot CLI][customize-cli]
- [使用 Copilot CLI 管理拉取请求][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
