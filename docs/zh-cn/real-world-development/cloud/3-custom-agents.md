---
title: "练习 3 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 的[自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的 AI 助手。你可以在存储库的 `.github/agents` 文件夹中创建 Markdown 文件，为 Copilot 提供聚焦的说明、最佳实践、编码模式和领域知识，帮助它更有效地完成特定工作。团队可将专业经验整理为可复用的智能体，例如执行 [WCAG][wcag] 要求的无障碍访问智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents` 文件夹中的 Markdown 文件定义，也可以在 `~/.copilot/agents` 中全局定义。每个文件都包含至少带有 `name` 和 `description` 字段的 YAML frontmatter，以及定义智能体行为、专长和说明的 Markdown 提示词。

### 自定义智能体与智能体技能的区别

自定义智能体与[智能体技能][agent-skills-concept]有些重叠：两者主要通过 Markdown 文件定义，并告诉 AI 如何执行任务。可以这样区分：**自定义智能体负责工作，技能提供工具**。

自定义智能体有自己的上下文窗口，能够协调技能（甚至其他智能体）来完成任务。本实验中的无障碍访问智能体会根据无障碍指南审查并更新网站；它可以调用拉取请求工作流技能或运行和管理测试的技能。

> [!NOTE]
> 编写自定义智能体没有唯一正确的方法。和其他 AI 功能一样，请在自己的环境和场景中测试并不断迭代。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

本课将介绍：

- 自定义智能体的定义方式；
- 如何将任务分配给自定义智能体。

## 场景

Tailspin Toys 致力于让所有用户都能使用其众筹平台，不受视力能力或偏好的影响。近期用户反馈指出，当前深色主题中的文字与背景对比度不足，难以阅读。设计团队因此要求添加可切换的高对比度模式。

无障碍访问至关重要，因此要尽快实现此功能。你将使用自定义智能体生成相关功能。

## 查看无障碍访问自定义智能体

项目已为无障碍访问创建自定义智能体。返回 codespace 并查看 `.github/agents/accessibility.md`：

1. 打开 `.github/agents/accessibility.md`。
2. 查看包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> `name` 和 `description` 是自定义智能体必需的 frontmatter 字段。

3. 浏览后续部分，了解其中的核心职责、无障碍访问最佳实践、HTML/CSS/JavaScript 代码示例，以及常见问题。

## 创建并分配议题

任务控制中心是管理环境中所有智能体的中心位置。可以在其中向云智能体分配任务、监控进度并提供额外指导。现在将创建高对比度模式的任务并分配给 Copilot：

1. 打开存储库。
2. 选择 **Issues** 选项卡，再选择 **New issue**。
3. 选择 **Blank issue**。
4. 将 **Title** 设置为 `Add high contrast mode to website`。
5. 将 **Description** 设置为：

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

6. 选择 **Create**。
7. 在右侧选择 **Assign to Copilot**，打开分配窗口。
8. 从列表中选择 **Accessibility agent**。

    ![在云智能体分配窗口中突出显示自定义智能体和无障碍访问智能体](../../../_images/ex5-select-custom-agent.png)

9. 选择 **Assign**。Copilot 会在后台开始处理任务。

## 总结和后续步骤

本课介绍了 GitHub Copilot 的[自定义智能体][custom-agents]，也就是针对特定任务和领域定制的 AI 助手。借助自定义智能体，团队可以将专业经验和标准整理为可复用的指导。

你已了解如何定义自定义智能体，以及如何将任务分配给它。

Copilot 正在实现高对比度模式。接下来前往[任务控制中心，监控并指导智能体会话][next-lesson]。

## 资源

- [关于自定义智能体][custom-agents]
- [为组织使用自定义智能体做准备][org-custom-agents]
- [为企业使用自定义智能体做准备][enterprise-custom-agents]

---

| [← 上一课：GitHub Copilot 云智能体][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
