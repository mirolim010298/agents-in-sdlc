---
title: "レッスン 8 - 機能 PR を作成してマージする"
description: "絞り込み、指示、スキル更新、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

絞り込みの実装、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストが、1 つのブランチに保存されています。これらをまとめてレビューし、プル リクエストを作成しましょう。星評価のプル リクエスト (PR) は自分でマージしましたが、今回は **Agent Merge** にマージの作業を任せます。

> [!NOTE]
> 通常は、機能、指示の更新、スキルの更新、QA エージェントを複数の PR に分けます。ワークショップを簡潔にするため、絞り込みと品質ワークフロー全体を 1 つの会話とブランチにまとめ、この PR に含めます。

このレッスンでは、次の操作を行います。

- Agent Merge と、マージ ライフサイクルを自動化する仕組みを学びます。
- 機能全体の変更と検証結果を確認します。
- 絞り込み PR を作成します。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認します。

## シナリオ

絞り込み機能の開発を通して、Copilot を使って機能を計画、実装、検証しました。Tailspin Toys では、マージを許可する権限は開発者が保持したまま、残りの PR 作業を自動化したいと考えています。

## Agent Merge とは

**Agent Merge** は、プル リクエストをマージするために必要な残りの作業を自動化します。有効にすると、Copilot は PR を妨げているもの (失敗した継続的インテグレーション (CI) チェックの修正、レビュー コメントへの対応、必要な場合のリベースなど) に取り組みます。その後、リポジトリで許可されていれば GitHub の自動マージを有効にします。

これまでは自分で **プル リクエストをマージ**を選択していました。Agent Merge にその作業を任せることができます。有効化する前に変更をレビューし、準備ができていることを確認してください。

## Agent Merge で PR を管理する

すべてのコードを作成できたので、まとめてレビューして PR を作成し、残りの作業を Agent Merge に任せます。

1. Codespace に戻ります。
2. `/agent` を実行してエージェントのダイアログを開きます。
3. 選択肢から **Default** を選び、<kbd>Enter</kbd> を押します。
4. `/pr create` コマンドを実行して PR を作成します。
5. `/pr agentmerge` を実行して Agent Merge を有効にします。
6. Copilot は PR の継続的インテグレーションの状況を監視し、すべて成功したらマージします。
7. `PR #14 was squash-merged successfully.` のような Copilot のメッセージが表示されたことを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージ キュー、リポジトリ設定、権限の不足を回避しません。処理がブロックされた場合は、報告された理由を確認し、リポジトリで許可されていれば、レビュー済みの変更を手動でマージしてください。

## まとめと次のステップ

コードの生成、テストと検証、プル リクエストの処理など、開発プロセスの一部を自動化しました。このレッスンでは、次の操作を行いました。

- Agent Merge と、マージ ライフサイクルを自動化する仕組みを学びました。
- 機能全体の変更と検証結果を確認しました。
- 絞り込み PR を作成しました。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認しました。

次は[GitHub Copilot CLI のスラッシュ コマンド][next-lesson]を確認し、コンテキスト、モデル、共有、任意のクラウド委任について学びます。

## リソース

- [Copilot CLI でプル リクエストを管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
