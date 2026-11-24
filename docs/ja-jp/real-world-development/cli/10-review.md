---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプル リクエスト、再利用できるカスタマイズ、参考資料を振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Tailspin Toys の一連の作業で GitHub Copilot CLI を使いました。次の操作を行いました。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトを確認し、登録済みの絞り込み issue を見つけました。
- 星評価を追加し、転送されたブラウザーで結果を確認して、最初のプル リクエスト (PR) を手動でマージしました。
- 絞り込みの issue から始め、Plan モードで方針を決め、Autopilot モードで実装し、Interactive モードでレビューしました。
- カスタム指示でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、単体テスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加して、実際のブラウザーで絞り込みを確認しました。
- 品質保証 (QA) カスタム エージェントを作成・選択し、要件、テスト範囲、スキルの結果、ブラウザーでの証拠を評価しました。
- 絞り込みの変更全体をレビューし、Agent Merge による絞り込み PR のマージを許可しました。
- コンテキスト、モデル、共有、クラウドへの任意の委任に使うスラッシュ コマンドを確認しました。

## リリースしたもの

ワークショップでは、更新済みの `main` からブランチを作成し、2 つの PR を行います。

1. **星評価**: 既存の `starRating` と未評価状態をゲーム カードに表示します。
2. **絞り込みと品質ワークフロー**: 絞り込みを実装し、指示を更新して機能に適用し、`quality-checks` レポートをカスタマイズし、QA プロファイルと関連テストを追加します。

絞り込みの計画から PR 作成まで、同じ会話とブランチを使いました。ワークショップを簡潔にするため、この作業を 1 つの PR にまとめました。

## さまざまな検証方法

自動テスト、自分で行うブラウザー確認、MCP を使った Copilot のブラウザー操作など、複数の方法でコードを確認しました。`quality-checks` スキルは単体テスト、lint、型チェックを実行し、新しい形式で結果を報告しました。QA はこれらの結果に加えて要件とテスト範囲をレビューしてから PR を作成しました。

追加するテストは、実際に不足している範囲を補うものである必要があります。QA の結果、テスト追加が不要な場合もあります。マージを許可する前にコードと証拠を確認し、変更後は影響する証拠を更新してください。

## ベスト プラクティス

Copilot に与えるコンテキストとツールが、作業結果を左右します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを設定しました。会話をまたいでカスタマイズを再利用し、チームのニーズに合わせて調整できます。指示は標準を設定し、スキルは繰り返し実行するタスクを記述し、カスタム エージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけではなく、実際の変更とツールの結果を確認してください。

タスクに合わせて**モードとモデル**を選択します。実装前に方針を検討するときは **Plan**、範囲を絞った変更を一緒に進めるときは **Interactive**、範囲が明確なタスクを任せるときは **Autopilot** を使います。定型的な編集には高速なモデルを、複雑な作業にはより高性能なモデルを選びます。

コンテキストは、インフラストラクチャと同じくらい重要です。何を、なぜ、どのように作るかを明確に説明すると、結果が大きく変わります。

## さらに試す

主要なワークフローを終えました。次の CLI 機能も確認してください。

- `/review` でコード レビュー エージェントに変更を分析させます。
- `/rubber-duck` で問題を説明し、別の視点を得ます。
- `/fleet` で独立したサブタスクを並行して調整します。
- `/worktree` で別のタスクを分離します。
- `/delegate` で Copilot cloud agent にタスクを委任します。

## 次のステップ

ツールのスキルを向上させる最善の方法は、使い続けることです。本番コード、趣味のコード、何年も作ろうと思っていた小さなアプリなどで活用してください。チームと学んだことを共有し、お互いの経験から学びましょう。ドキュメントも引き続き確認してください。

ターミナルから Tailspin Toys を拡張する場合は、任意の [Foundry Backer Concierge シリーズ][foundry]に進みます。別の環境も確認する場合は、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、[Copilot cloud agent ワークショップ][cloud]をご覧ください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプル リクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
