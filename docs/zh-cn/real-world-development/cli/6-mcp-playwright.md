---
title: "第 6 课 - 使用 Playwright MCP 验证功能"
description: "在 Copilot CLI 中配置 Playwright MCP，并在浏览器中检查筛选功能。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

编写代码只是开发工作的一部分。还需要处理数据、外部服务，并为 Copilot 提供额外自动化能力。MCP 服务器可以扩展 Copilot CLI 内置功能，让它使用更多工具和服务。

本课将介绍 Model Context Protocol (MCP)、Copilot CLI 如何使用 MCP、如何添加 Playwright MCP 服务器，以及如何让智能体在浏览器中检查筛选功能。

## 场景

单元测试和端到端测试很重要，但验证 UI 更新还需要实际与界面交互。现在让 Copilot 像用户一样操作网站，以自动检查功能是否符合预期。

## 什么是 Model Context Protocol (MCP)？

[Model Context Protocol (MCP)][mcp-blog-post]让 AI 智能体能够与外部工具和服务通信，实时获取信息并代表你执行操作。MCP 服务器充当智能体与外部工具之间的桥梁，每个服务器提供一组可访问的工具和资源。

常见服务器包括：

- **[GitHub MCP Server][github-mcp]**：提供管理 GitHub 存储库、议题和拉取请求的 API。
- **[Playwright MCP Server][playwright-mcp-server]**：提供 Playwright 浏览器自动化能力。

还有许多其他 MCP 服务器。GitHub 提供 [MCP 注册表][mcp-registry]，帮助发现并参与生态系统。

> [!CAUTION]
> 应像对待项目的其他依赖项一样对待 MCP 服务器。使用前审查源代码、验证发布者并评估安全影响。

## 添加 Playwright MCP 服务器

如果 Copilot CLI 尚未配置 Playwright MCP，请按以下步骤添加。若已配置，可跳过本节。

1. 返回 Codespace。
2. 在 Copilot CLI 中输入以下命令打开添加 MCP 服务器对话框：

   ```plaintext
   /mcp add
   ```

3. 名称输入 `playwright`，再按 <kbd>Tab</kbd>。
4. 按 <kbd>Enter</kbd> 确认服务器类型为 **STDIO**，再按 <kbd>Tab</kbd>。
5. 在 **Command** 对话框中输入：

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. 按 <kbd>Control</kbd>+<kbd>S</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>S</kbd>（Windows/Linux）保存服务器。
7. 按 <kbd>Esc</kbd> 退出 MCP 对话框。

## 让 Copilot 使用 Playwright 探索功能

之前已手动确认功能行为正常。现在使用 Copilot 中的 Playwright MCP 服务器完成同样的检查：

1. 发送以下提示：

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> 通常 Copilot 会自动找到 MCP 服务器并使用它，但明确指出工具有助于获得更一致的结果，也能减少额外探索。

2. 观察 Copilot 在浏览器中执行的各项操作。
3. 阅读报告，确认功能行为符合预期。

Copilot 会启动服务器，通过 Playwright 操作网站，停止服务器并返回报告。

## 总结和后续步骤

你已使用 Playwright MCP 服务器，让 Copilot CLI 在真实浏览器中检查功能，并了解 MCP 及其在 Copilot CLI 中的用途。接下来创建[质量保证自定义智能体][next-lesson]，将技能与浏览器工具结合起来。

## 资源

- [MCP 是什么，为什么大家都在讨论？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [向 Copilot CLI 添加 MCP 服务器][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
