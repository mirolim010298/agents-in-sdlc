---
slug: ja-jp/real-world-development/vscode
title: "Visual Studio Code"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の **[GitHub Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/copilot-chat)** から、普段使っているコード エディターで GitHub Copilot を利用できます。Visual Studio Code と GitHub Codespaces で Copilot Chat のエージェント モードを使い、MCP で外部ツールに接続し、カスタム エージェントを活用します。IDE を離れずに、Copilot がファイル、ターミナル、問題を確認できます。

最初にカスタム指示を追加し、Copilot が指示に従う様子を確認します。次にエージェント モードで UI、データ レイヤー、テストにわたる絞り込み機能を実装します。Playwright MCP サーバーを接続し、ブラウザーで機能をテストしてからプル リクエストを作成します。最後にアクセシビリティ用のカスタム エージェントを確認して使い、エディターを離れずに Copilot の変更を監視、案内、反復します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成します |
| [1. カスタム指示][ex1] | コンテキスト | VS Code でカスタム指示を追加して確認します |
| [2. エージェント モード][ex2] | コード生成 | エージェント モードで絞り込み機能を作成します |
| [3. Playwright MCP][ex3] | 外部ツール | Playwright MCP サーバーでブラウザーから機能をテストします |
| [4. カスタム エージェント][ex4] | 専門エージェント | カスタム エージェントを確認して使います |
| [5. エージェントの管理][ex5] | 監視 | エージェント セッションを監視して案内します |
| [6. 反復][ex6] | レビュー | Copilot の作業をレビューし、次の手順を選びます |
| [任意: Foundry を取り入れる][foundry-toolkit] | AI エージェント | VS Code と Foundry Toolkit を使う 3 つのモジュールで、モデルを準備し、エージェントをデプロイしてサイトに接続します |

## 前提条件

ワークショップに参加する前に、次の準備をしてください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** プランの GitHub アカウント
- [ ] GitHub Codespaces へのアクセス

> [!TIP]
> 有料プランをお持ちでない場合、認定学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コード レビュー、Copilot CLI の機能が含まれるため、すべてのハーネスを完了できます。

[callout-student-plan-education]: https://github.com/education/students

## 開始する

**[演習 0: 前提条件から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-agent-mode/
[ex3]: 3-mcp/
[ex4]: 4-custom-agents/
[ex5]: 5-managing-agents/
[ex6]: 6-iterating/
[foundry-toolkit]: 7-foundry-toolkit/
