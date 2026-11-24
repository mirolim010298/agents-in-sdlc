---
title: "练习 4 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 的[自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的 AI 助手。通过在存储库 `.github/agents` 文件夹中创建 Markdown 文件，可以提供聚焦的说明、最佳实践、编码模式和领域知识。团队可以将专业经验整理为可复用智能体，例如执行 [WCAG][wcag] 要求的无障碍访问智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents` 文件夹中的 Markdown 文件定义，也可以全局定义在 `~/.copilot/agents` 中。文件需包含至少带有 `name` 和 `description` 字段的 YAML frontmatter，以及定义行为、专长和说明的 Markdown 提示词。

### 自定义智能体与智能体技能

自定义智能体和[智能体技能][agent-skills-concept]都有些相似：两者主要通过 Markdown 文件定义，并告诉 AI 如何执行工作。最简单的区分方式是：**自定义智能体负责工作，技能提供工具**。

自定义智能体拥有自己的上下文窗口，可协调技能甚至其他智能体完成任务。本实验中的无障碍访问智能体会根据无障碍指南审查并更新网站，也可以调用拉取请求工作流技能或测试管理技能。

> [!NOTE]
> 编写自定义智能体没有唯一正确的方法。请根据自己的环境和场景进行测试和迭代。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## 场景

Tailspin Toys 希望让所有用户都能使用众筹平台，不受视力能力或偏好的影响。用户反馈指出，当前深色主题中的文字与背景对比度不足，难以阅读。设计团队因此要求添加可切换的高对比度模式。

本练习将介绍自定义智能体的定义方式，以及如何在 Copilot Chat 中使用无障碍访问智能体来实现高对比度模式。

## 查看无障碍访问自定义智能体

项目已为无障碍访问准备了自定义智能体。返回 codespace 并从 `main` 创建新分支，将无障碍访问工作与练习 3 中的筛选 PR 分开：

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. 打开 `.github/agents/accessibility.md`。
2. 查看带有 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> `name` 和 `description` 是自定义智能体必需的 frontmatter 字段。

3. 浏览后续部分，了解生成无障碍网站代码时的核心职责、无障碍最佳实践、HTML/CSS/JavaScript 示例，以及常见问题。

## 在 Copilot Chat 中使用自定义智能体

VS Code 会在 Copilot Chat 底部的智能体下拉列表中显示 `.github/agents` 目录里的自定义智能体。选择自定义智能体后，该会话会遵循相应说明和工具配置。

> [!TIP]
> **打开 Copilot Chat**
>
> 返回 codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。请按步骤说明选择模式和模型。

1. 在 Chat 视图的智能体下拉列表中选择 **Agent**（如果尚未选择）。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

2. 选择 Chat 视图底部的智能体下拉菜单（默认显示 **default**）。
3. 从可用智能体列表中选择 **Accessibility agent**。
4. 发送以下提示：

    ```plaintext
    Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
    ```

5. Copilot Chat 会探索代码库、提出更改并修改项目文件。每项编辑都会以内联差异的形式显示文件路径和更改内容。
6. 编辑过程中，**Files changed** 指示器会更新，显示智能体修改的文件。

> [!NOTE]
> 该过程可能需要几分钟。Copilot 会修改 Astro 组件、CSS 和相关测试等现有文件。

下一课将审查并指导进行中的工作。

## 总结和后续步骤

本课介绍了 GitHub Copilot 的[自定义智能体][custom-agents]，也就是为特定任务或领域定制的 AI 助手。你已了解如何定义自定义智能体，以及如何在 Copilot Chat 智能体模式中使用它。

下一步[监控并指导智能体工作][next-lesson]：审查正在产生的更改，并在同一会话中添加浅色模式开关。

## 资源

- [关于自定义智能体][custom-agents]
- [在 IDE 中创建自定义智能体][creating-custom-agents-ide]
- [VS Code 中的自定义智能体][custom-agents-vscode]
- [自定义智能体配置][custom-agents-config]
- [Awesome Copilot 上的自定义智能体][awesome-copilot-agents]

---

| [← 上一课：使用 Playwright MCP 测试功能][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
