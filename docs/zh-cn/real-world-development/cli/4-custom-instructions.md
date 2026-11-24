---
title: "第 4 课 - 使用自定义说明指导 Copilot"
description: "浏览存储库说明、添加文档标准，并将其应用到筛选代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式 AI 时，上下文至关重要。任务可能需要特定做法，因此应让 Copilot 能访问相关指导。[说明文件][instruction-files]不仅描述想要什么代码，也说明代码应如何组织。现在已实现筛选功能，接下来查看 Copilot 使用的说明、添加文档标准并将其应用到代码中。

本课将介绍如何查看存储库和路径级说明、更新说明以确保遵循编码标准，以及观察说明文件对代码的影响。

## 场景

Tailspin Toys 的开发实践要求包括：

- 注释应解释意图和不明显的决策，而不是复述代码；
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明用途、参数和返回值（包括可注入的 `db` 参数）；
- 可复用 Astro 组件应说明其 `Props` 接口；相关代码更改时，注释也应保持更新；
- 保留现有格式和 lint 指南。

使用说明文件确保 Copilot 了解并遵循这些实践。

## 说明文件

自定义说明可以为 Copilot 提供上下文和偏好，帮助它了解编码风格和需求。可以为整个存储库创建说明，也可以为特定语言、文件类型或任务提供指导：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送此文件，适合存放常用项目级信息。
- `.github/instructions/*.instructions.md`：为特定语言、文件类型或任务提供指导。

> [!NOTE]
> 其他说明格式及其支持情况因环境而异。依赖特定格式前，请查看[自定义说明支持参考][custom-instructions-support]。

## 浏览本项目中的自定义说明文件

启动项目时已包含一组说明文件。先浏览这些文件，再进行更改：

1. 返回 Codespace。
2. 在 Codespaces 编辑器（不是终端）中打开 `.github/copilot-instructions.md`。
3. 浏览项目简介和编码指导。此文件适用于该存储库中与 Copilot 的每次交互。
4. 打开 `.github/instructions` 文件夹，查看针对 Astro、Drizzle 数据层和测试等内容的说明。
5. 打开 `.github/instructions/unit-tests.instructions.md`，查看顶部决定说明适用文件的 `applyTo` 字段。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看它对其他说明文件和项目现有文件的引用。这样可以拆分较大的说明集并提供示例。

## 更新说明以符合团队指导

当前说明文件已包含许多规范，但还未要求新生成的 TypeScript 添加 TSDoc 注释。现在更新核心 `copilot-instructions.md`：

1. 找到 **Code formatting guidance** 部分，通常在第 35 行附近。
2. 在最后一条之后添加：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

文件会自动保存。

## 使用更新后的指导

Copilot CLI 在新会话开始时加载存储库说明。保存更新后，退出并恢复筛选会话，使 Copilot 加载新说明，同时保留功能上下文。

1. 如果筛选对话仍打开，输入 `/exit`。Copilot CLI 会自动保存会话。
2. 在存储库根目录的 `game-filters-cli` 分支中恢复会话：

   ```bash
   copilot --resume
   ```

   如果出现提示，选择筛选会话并确认当前检出的是 `game-filters-cli` 分支。
3. 让 Copilot 应用更新后的指导：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff`，检查更改的 TypeScript 文件。确认新 TSDoc 注释准确说明代码行为。

## 总结和后续步骤

你了解了 Copilot CLI 如何读取说明文件，并将新标准应用到筛选功能中。接下来[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保一致地运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义说明][instruction-files]
- [自定义说明支持][custom-instructions-support]
- [创建自定义说明的最佳实践][instructions-best-practices]
- [Awesome Copilot——说明文件及其他资源集合][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
