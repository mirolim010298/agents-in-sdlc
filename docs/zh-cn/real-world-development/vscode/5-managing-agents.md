---
title: "练习 5 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义智能体][previous-lesson] |
|:--|

Copilot 智能体模式会自主探索代码库、提出更改、编辑文件并运行命令。VS Code 中的 Copilot Chat 会实时显示工具调用和文件编辑。你可以查看内联差异、逐项接受或撤销更改，并用后续提示调整工作，而无需离开编辑器。

本练习将介绍如何实时监控无障碍访问智能体、审查并接受文件编辑，以及指导智能体在高对比度模式旁添加浅色模式开关。

## 场景

[练习 4][previous-lesson]中的无障碍访问自定义智能体正在实现高对比度模式。工作期间，设计团队又提出增加浅色模式切换开关的要求。无需重新开始对话，直接引导当前会话扩展工作。

## 监控 Copilot 进度

Copilot Chat 会显示智能体执行的每个步骤，包括探索的文件、运行的命令和建议的编辑。每项编辑都会以内联差异形式显示，并提供 **Keep** 和 **Undo** 控件。

1. 返回练习 4 中的 Copilot Chat 视图。
2. 随着智能体工作，滚动聊天记录查看工具调用、文件读取、编辑和请求运行的终端命令。
3. 审查内联差异：
   - 选择 **Keep** 接受更改；
   - 选择 **Undo** 撤销更改，让智能体重新尝试。
4. 选择聊天顶部的 **Files changed** 指示器，查看本次会话中修改的完整文件列表。

> [!NOTE]
> 如果工具调用需要权限（例如运行终端命令），智能体会暂停并显示 **Allow** 提示。只批准你认可的命令。

5. 等待智能体完成高对比度模式，并查看它对更改的总结。

## 指导智能体添加浅色模式

高对比度模式完成后，在同一对话中添加浅色模式。由于继续使用相同会话，智能体会保留之前的上下文，包括修改的组件、样式方法和本地存储模式。

1. 在 Copilot Chat 输入框中发送以下后续提示：

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. 智能体会查看已做的更改，并提出浅色模式的补充内容。
3. 像审查高对比度模式一样，逐项检查新编辑并选择 **Keep** 或 **Undo**。
4. 如果智能体的方向不符合预期（例如尝试重构切换 UI），可以选择输入框旁的 **Stop** 按钮停止任务，然后发送澄清提示。

> [!TIP]
> 指导进行中的会话通常比从头开始更快。可以用后续提示要求简化 CSS、使用 CSS 变量、将浅色模式整合进现有设置面板，或为两个开关添加键盘快捷键。

## 审查工作集

提交之前，快速检查智能体修改的所有内容：

1. 在 VS Code 中打开 **Source Control** 视图。
2. 查看所有更改的文件，包括 Astro 组件、样式和相关测试。
3. 打开几个文件检查差异，确认无障碍模式包含 ARIA 属性、键盘导航、语义化 HTML，并使用本地存储保存偏好。
4. 满意后，在 Source Control 面板暂存并提交更改。下一课会发布这些更改。

## 总结和后续步骤

你使用 Copilot Chat 智能体模式监控并指导进行中的会话，审查每项文件编辑、接受或撤销更改，并在保留上下文的同时发送后续提示扩展工作。

你已了解实时监控智能体工作、接受或撤销单项编辑，以及在会话进行时指导智能体。下一课会将无障碍访问工作发布为拉取请求，并审查本实验中本地自定义智能体生成的更改。

## 资源

- [VS Code 中的 Copilot Chat][copilot-chat-vscode]
- [使用智能体模式][agent-mode]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代完善 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
