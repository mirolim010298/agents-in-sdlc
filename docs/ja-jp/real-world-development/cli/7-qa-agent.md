---
title: "レッスン 7 - QA エージェントを作成して使う"
description: "issue の要件、quality-checks スキル、Playwright MCP を組み合わせた QA カスタム エージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright MCP でブラウザー上の絞り込みを確認しました。今度は、これらの機能を明確な QA プロセスを持つカスタム エージェントにまとめます。

このレッスンでは、次の操作を行います。

- カスタム エージェントが指示、スキル、MCP ツールを活用する仕組みを確認します。
- 再利用可能な品質保証プロファイルを作成して確認します。
- QA エージェントを選び、絞り込みの issue に基づく結果をレビューします。

## シナリオ

Tailspin Toys では、プル リクエスト (PR) を作成する前に、要件、コード品質、自動チェック、テスト範囲、ブラウザーでの動作を一貫してレビューしたいと考えています。カスタム エージェントを使えば QA プロセスをまとめ、再利用できるレポートを作成できます。

## カスタム エージェントとは

カスタム エージェントは、Markdown プロファイルで定義する専門化された Copilot です。エージェントの目的、指示、使用可能なツールを記述します。このワークショップでは `.github/agents/qa.agent.md` に QA の役割を定義し、Copilot CLI で選択します。

これまでに使ったカスタマイズには、それぞれ異なる役割があります。リポジトリの指示はチームの標準を説明します。`quality-checks` スキルは繰り返し実行できるチェックをまとめます。Playwright MCP はブラウザー ツールを提供します。QA プロファイルは、それらを使って要件を評価し、結果を報告するよう Copilot に伝えます。カスタム エージェントは各機能の代わりではなく、別の会話も必要ありません。

## QA プロファイルを作成する

機能 PR を開く前に、再利用可能な QA プロファイルの作成を Copilot に依頼します。QA が行うチェックと守るべき範囲の両方を定義します。

1. Codespace に戻り、絞り込みの会話が Interactive モードであることを確認します。
2. デフォルト エージェントに、次のカスタム エージェントを作成するよう依頼します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

エージェントを使う前に、意図した QA ワークフローと境界が正しく含まれていることを確認します。確認によって、検証だけを依頼したのに不完全であったり、範囲が広すぎて機能を変更したりするのを防げます。

1. `/diff` を実行し、`.github/agents/qa.agent.md` を開きます。
2. フロントマターを読みます。`description` は必須です。`name` は任意ですが、表示名としてわかりやすくなります。
3. プロファイルの指示を読み、QA が要件を起点にし、リポジトリの指示に従い、`quality-checks` スキルと Playwright MCP を使うことを確認します。
4. QA が根拠を示して報告し、実装コードの変更前に確認を求め、コミットやプル リクエストの作成を行わないことを確認します。
5. 責任や境界が不足していたら、続行前にデフォルト エージェントへ修正を依頼します。

## issue に対して QA を実行する

Copilot CLI は会話の開始時にプロジェクト エージェントを読み込みます。プロファイルを作成したら同じ絞り込みの会話を再開し、QA を選択して、issue と計画の決定を利用できるようにします。

1. 次のプロンプトでエージェントを有効にします。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> エージェントを作成した直後は、利用可能なエージェントの一覧に表示されない場合があります。上のコマンドを使えば有効化できます。

2. QA エージェントに機能をレビューするよう依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントが作業する様子を確認します。
4. 完了したら、レポートを読みます。

## まとめと次のステップ

再利用可能な専門的役割をワークフローに加え、結果をレビューしました。このレッスンでは、次の操作を行いました。

- カスタム エージェントが指示、スキル、MCP ツールを活用する仕組みを確認しました。
- 再利用可能な品質保証プロファイルを作成して確認しました。
- QA エージェントを選び、issue に基づく結果をレビューしました。

実装、スキルの更新、QA プロファイル、テスト、検証レポートが揃いました。次は[機能 PR を作成して Agent Merge を使います][next-lesson]。

## リソース

- [Copilot CLI 用のカスタム エージェントを作成する][create-agents]
- [カスタム エージェントの設定][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
