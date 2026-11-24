---
title: "练习 0：准备工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 VS Code 练习前，先创建 Tailspin Toys 存储库副本、启动 [codespace][codespaces]，并确认编辑器中的 GitHub Copilot Chat 可正常使用。

## 设置实验存储库

1. 在新浏览器窗口中打开 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面选择 **Use this template**，再选择 **Create a new repository**。

    ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果你正在参加 GitHub 或 Microsoft 举办的活动，请遵循导师提供的说明。否则，可以在你有权使用 GitHub Copilot 的组织中创建存储库。

    ![填写存储库模板设置](../../../_images/ex0-repository-settings.png)

4. 记下存储库路径（**organization-or-user-name/repository-name**），稍后会用到。

> [!NOTE]
> 从模板创建存储库时，系统会自动为你创建一组 GitHub 议题作为待办事项。本研讨会会使用这些议题，无需自行创建。

## 创建 codespace

[GitHub Codespaces][codespaces] 是基于云的开发环境，可让你直接在浏览器中编写、运行和调试代码，并提供支持多种编程语言、扩展和工具的完整 IDE。

1. 打开刚创建的存储库。
2. 选择绿色的 **Code** 按钮。

    ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，再选择 **+** 按钮创建新的 Codespace。

    ![创建新的 codespace](../../../_images/ex0-create-codespace.png)

codespace 创建需要几分钟，但比手动安装所有服务快得多。等待时可以了解 GitHub Copilot 的其他功能。

> [!CAUTION]
> 后续练习会继续使用此 codespace。现在请在浏览器选项卡中保持打开。

> [!NOTE]
> 本研讨会可在 codespace 或本地 [dev container][dev-containers] 中运行，两者都已包含所需先决条件。如需在本地运行，请在 VS Code 中打开克隆的存储库，并在提示出现时选择 **Reopen in Container**。VS Code 将构建与 codespace 相同的 dev container。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 使用 GitHub Copilot Chat 和智能体模式

要在 IDE 中使用 GitHub Copilot Chat 智能体模式，需要安装 GitHub Copilot Chat 扩展。使用 GitHub Codespaces 时，该扩展通常已安装。

> [!TIP]
> 如果尚未安装 GitHub Copilot Chat 扩展，可以从 [Visual Studio Code Marketplace][copilot-chat-extension] 安装；也可以在 Visual Studio Code 的扩展视图中搜索 **GitHub Copilot Chat** 并选择 **Install**。

安装扩展后，可能需要使用 GitHub 帐户登录：

1. 返回 codespace。
2. 如果编辑器右侧没有显示 Copilot Chat，选择 codespace 顶部的 **Copilot Chat** 图标。
3. 在 Copilot Chat 中输入 `Hello world` 并按 Enter，启动 Copilot Chat。
4. 如果尚未登录，请按照提示使用 GitHub 帐户完成身份验证。
5. 登录后，Copilot Chat 窗口会显示在编辑器中。

    ![Copilot Chat 身份验证提示示例](../../../_images/ex1-copilot-authentication.png)

## 总结

你已创建实验存储库副本并开始创建 codespace，后续会在其中编写代码。

## 下一步

继续学习[练习 1 - 自定义说明][next-lesson]，向 Copilot 介绍项目约定。

## 资源

- [GitHub Codespaces 概览][codespaces]
- [根据模板创建存储库][template-repository]
- [Codespaces 入门][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
