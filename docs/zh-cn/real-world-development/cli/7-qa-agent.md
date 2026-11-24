---
title: "第 7 课 - 创建并使用 QA 智能体"
description: "创建结合议题需求、quality-checks 技能和 Playwright MCP 的 QA 自定义智能体。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动检查，并通过 Playwright MCP 在浏览器中查看筛选体验。现在将这些能力整合到一个定义清晰的 QA 流程和自定义智能体中。

本课将介绍如何让自定义智能体结合说明、技能和 MCP 工具，创建并检查可复用的质量保证配置，并根据筛选议题审查结果。

## 场景

Tailspin Toys 希望在创建拉取请求（PR）前，一致地审查需求、代码质量、自动化检查、测试覆盖率和浏览器行为。自定义智能体可以协调 QA 流程并生成可复用报告。

## 什么是自定义智能体？

自定义智能体是通过 Markdown 配置文件定义的 Copilot 专用角色，文件会说明用途、指导和可用工具。本研讨会会在 `.github/agents/qa.agent.md` 中定义 QA 角色，并在 Copilot CLI 中选择它。

之前使用的自定义能力各有不同用途：存储库说明描述团队标准；`quality-checks` 技能封装可重复检查；Playwright MCP 提供浏览器工具；QA 配置则指导 Copilot 如何运用这些能力评估需求并汇报结果。它们无需互相替代，也不必切换到另一个对话。

## 创建 QA 配置

创建功能 PR 前，让 Copilot 创建可复用的 QA 配置，并明确 QA 要执行的检查和必须遵守的边界。

1. 返回 Codespace，确认筛选对话处于 Interactive 模式。
2. 请默认智能体创建自定义智能体：

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## 检查配置文件

使用新智能体前，先确认 Copilot 捕获了预期的 QA 流程和限制，避免它在只要求验证时修改功能。

1. 输入 `/diff` 并打开 `.github/agents/qa.agent.md`。
2. 查看 frontmatter。`description` 为必填项；`name` 是可选项，但可以设置清晰的显示名称。
3. 检查说明是否要求 QA 从需求出发、遵循存储库说明、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会提供支持证据、修改实现代码前会先询问，而且不会提交代码或创建 PR。
5. 如果缺少任何职责或限制，请先让默认智能体修改配置。

## 根据议题运行 QA

Copilot CLI 在会话开始时加载项目智能体。创建配置后恢复筛选会话，再选择 QA，以便它使用已有的议题和计划决定。

1. 输入以下命令启用智能体：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 新创建的智能体可能不会立即出现在可用列表中，但仍可通过上述命令启用。

2. 发送以下提示，让 QA 审查功能：

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. 等待 QA 智能体执行检查。
4. 阅读它生成的报告。

## 总结和后续步骤

你已将可复用的专家角色加入工作流，并审查了它的结果。你了解了自定义智能体如何结合说明、技能和 MCP 工具，创建并检查 QA 配置，并针对筛选议题审查结果。

现在实现、技能更新、QA 配置、测试和验证报告都已准备好。下一步将它们[汇总到功能 PR 中并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义智能体][create-agents]
- [自定义智能体配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
