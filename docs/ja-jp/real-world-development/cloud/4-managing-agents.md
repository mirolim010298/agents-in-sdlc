---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前の 2 つの演習では、ユーザー エクスペリエンスの改善や機能追加を目的とする 3 つのタスクを Copilot cloud agent に依頼しました。cloud agent は非同期かつ自律的に作業しますが、タスクを監視することも重要です。

cloud agent に割り当てたタスクは、GitHub.com の[エージェント ページ][agents-page]など、さまざまなツールで管理できます。この Mission control では、オープン中のプル リクエスト (PR) があるすべてのエージェント タスクを確認できます。実行内容を調べ、進行中のセッションに追加の指示を伝えられます。

このレッスンでは、次の操作を行います。

- エージェント ページで cloud agent のタスクを監視します。
- セッションに追加の機能を依頼します。

## シナリオ

チームは、ハイ コントラスト モードに加えてライト モードも追加するとよいと気づきました。サイトのスタイルと切り替え機能を更新しているため、同時に追加するのが自然です。エージェントの作業を案内し、両方のモードを追加させます。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたすべてのタスクの状態を確認しましょう。

1. [Copilot agents ページ](https://github.com/copilot/agents)に移動します。
2. メイン ペインと左ペインのタスクリストを確認します。次のようなタスクが表示されます。
   - コードベースのドキュメントを更新する。
   - ゲーム変更用の API を生成する。
   - Web サイトにハイ コントラスト モードを追加する。
3. 実行中のタスクを選択し、Copilot が行った操作を確認します。次のような操作があります。
   - リポジトリからコードをチェックアウトする。
   - Copilot 用の環境を作成する。
   - MCP サーバーを設定する。
   - タスクを完了するためにさまざまな手順を実行する。

> [!NOTE]
> 表示される手順は、Copilot の作業状況と実装方法によって異なります。

4. 右側に表示されるプル リクエスト (PR) ペインも確認します。PR と変更されたファイルを監視できます。

## cloud agent に追加の指示を伝える

有効なタスクを確認したので、ハイ コントラスト モードに取り組んでいる Copilot にライト モードの追加も依頼します。

1. ハイ コントラスト モードのセッションを選択します。正確なタイトルは Copilot が付けた名前や作業状態によって異なります。

   ![Mission control のアクセシビリティ セッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了し作業を始めるまで数分待ちます。セッションにメッセージが表示されたら作業開始の目安です。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![エージェント ページの Copilot タスクに表示される「Steer active session while Copilot is working」ダイアログ](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot が指示を受け取り、作業に含めることを確認します。

## Copilot に作業を続けさせる

前と同じように、Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で作業していた手順が終わると、新しい依頼をワークフローに組み込みます。

今回も数分かかります。これまでに学んだ内容を振り返りましょう。

## まとめと次のステップ

Copilot agents ページを使って、GitHub Copilot cloud agent のタスクを監視し、案内する方法を学びました。Mission control では、進行中と完了済みのタスク、実行中の作業を確認し、処理中のタスクに追加の指示を与えられます。

このレッスンでは、次の操作を行いました。

- Mission control とエージェント ページを使って cloud agent のタスクを監視しました。
- 進行中のセッションに追加の機能を依頼しました。

Copilot がアクセシビリティ機能を実装している間に、[Copilot が作成したプル リクエストを反復して改善します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタム エージェントについて][custom-agents]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
