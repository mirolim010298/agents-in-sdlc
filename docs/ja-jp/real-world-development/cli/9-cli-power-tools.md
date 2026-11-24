---
title: "レッスン 9 - GitHub Copilot CLI のスラッシュ コマンド"
description: "コンテキストの管理、モデルの選択、セッションの共有、任意のクラウド委任に使うスラッシュ コマンドを確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

多くの CLI ツールと同様に、GitHub Copilot CLI にもさまざまなスラッシュ コマンドがあります。これらのコマンドを使うと、高度な機能、内部情報、追加の構成オプションを利用できます。これまで `/diff`、`/mcp`、`/skills`、`/agent`、`/pr` などを使いました。ここでは、ほかの便利なコマンドを確認します。

このレッスンでは、次の操作を行います。

- `/context` と `/compact` を使い、Copilot が会話のコンテキストを管理する方法を確認します。
- `/model` で利用可能なモデルを確認します。
- `/share` を使ってセッションをエクスポートまたは共有する方法を学びます。
- 並行作業、worktree、クラウド エージェントへの委任に使う任意のコマンドを確認します。

## シナリオ

CLI の主要なワークフローを終えました。ここでは、コンテキストの管理、モデルの切り替え、セッションの共有、[Copilot cloud agent][about-cloud-agent]への任意の委任など、追加機能を確認します。

## Copilot CLI のコンテキストを確認する

規模の大きいタスクや複雑なタスクでは、モデルの最大コンテキスト ウィンドウに達することがあります。Copilot CLI は必要に応じて会話を自動的に圧縮します。スラッシュ コマンドを使えば、状態の確認や手動での圧縮もできます。

1. Codespace に戻ります。Copilot CLI が開いていない場合は、リポジトリのルートから起動します。
2. 次のコマンドを入力します。

   ```plaintext
   /context
   ```

3. モデル、現在のトークン使用量、システム指示、ツール、メッセージ、空き領域に分割されたコンテキストを確認します。
4. 会話を圧縮します。

   ```plaintext
   /compact
   ```

5. もう一度 `/context` を実行して結果を比べます。会話が短い場合は、大きな違いがないこともあります。

> [!NOTE]
> コンテキスト ウィンドウが埋まると、Copilot CLI は自動的に内容を圧縮します。タイミングを自分で決めたい場合は `/compact` を実行します。無関係なタスクに切り替えて新しい会話を始める場合は、`/clear` または `/new` を使います。

## モデルを選ぶ

モデルごとに得意分野が異なり、開発者によって好みも異なります。Copilot CLI では、利用可能なモデルを一覧表示して選択できます。

1. 次のコマンドを入力します。

   ```plaintext
   /model
   ```

2. 利用可能なモデルと使用状況を確認します。
3. 現在のモデルを維持するか、別のモデルを選ぶか、<kbd>Esc</kbd> を押して一覧を閉じます。

## セッションを共有する

チームで協力し、知識を共有すると、AI ツールをより活用できます。`/share` コマンドでは、セッションを Markdown または HTML ファイルにエクスポートしたり、共有リンクを作成したり、GitHub gist を公開したりできます。

1. `/help` を実行し、インストール済みバージョンで利用できる `/share` オプションを確認します。
2. セッションを共有する場合は、目的に合った方法を選びます。たとえば `/share file` はローカルの Markdown ファイルにエクスポートします。
3. エクスポートした内容には、プロンプト、応答、プロジェクトの詳細が含まれる場合があります。誰かに送信したり公開したりする前に、内容を確認してください。

リンクや gist の公開は任意です。チームが共有するつもりのないリポジトリや会話の内容を公開しないでください。

## 任意: 作業を拡張または委任する

ワークショップの主要な部分は完了です。Copilot CLI には、大規模なタスクに役立つ次のコマンドもあります。

- `/fleet` は、独立したサブタスクをサブエージェントに分割して並行実行できます。
- `/worktree` は、別のタスク用に分離された Git worktree を作成できます。
- `/delegate` は、Copilot cloud agent にタスクを委任できます。エージェントは非同期で作業し、プル リクエストを作成することがあります。

これらのコマンドは追加の worktree やリモート作業を作成する場合があるため、任意です。試す場合は、範囲を明確にした新しいタスクから始め、通常のワークフローで結果をレビューしてください。非同期エージェントの作業を詳しく知りたい場合は、[cloud agent ワークショップ][cloud-workshop]に進んでください。

## まとめと次のステップ

Copilot CLI のスラッシュ コマンドを使うと、設定を変更し、セッションを共有し、内部の状況を確認できます。このレッスンでは、次の操作を行いました。

- `/context` と `/compact` でコンテキスト管理を確認しました。
- `/model` で利用可能なモデルを確認しました。
- `/share` でセッションをエクスポートまたは共有する方法を学びました。
- 並行作業、worktree、cloud agent への任意の委任コマンドを確認しました。

ほかにも多くのスラッシュ コマンドがあります。次は[学んだことと今後のステップを振り返り][next-lesson]、Copilot CLI での学習を続けましょう。

## リソース

- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のコンテキスト管理][context-management]
- [Copilot cloud agent について][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
