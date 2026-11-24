---
title: "レッスン 3 - エージェント モード: Plan と Autopilot"
description: "Plan で方針を合意し、Autopilot で issue から絞り込み機能を実装して、Interactive モードで結果をレビューします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

最初に小さな機能をプロジェクトに追加しました。より大きな変更には、しっかりしたプロセスが必要です。GitHub Copilot CLI は組織の既存のフローに沿って動作するよう設計されているため、適切な方法で必要なものを構築できます。ここから数レッスンにわたり、issue を起点に機能を実装し、コードの妥当性と機能の動作を確認し、最後にプロジェクトへマージする、一般的なエージェント主導の開発プロセスを進めます。

> [!NOTE]
> 機能開発の間は、同じ会話とブランチを使います。通常、ファイルの種類ごとにブランチや PR を分けますが、ここでは基本概念に集中するため簡略化します。

このレッスンでは、次の操作を行います。

- GitHub issue から新しい Copilot の会話を開始します。
- Plan モードで要件を定義します。
- Autopilot モードで新しい機能を実装します。
- コードをレビューします。
- 転送されたブラウザーで機能を手動検証します。

この機能の開発を続ける中で、リポジトリの指示を更新し、既存の `quality-checks` スキルをカスタマイズし、MCP 検証を追加して QA エージェントを作成し、機能 PR を作成します。

## シナリオ

Tailspin Toys のカタログが増えているため、訪問者がゲームをカテゴリや販売元で絞り込めるようにする必要があります。バックログの issue には機能が記されていますが、カテゴリを組み合わせる方法など、コーディング前に合意すべき詳細があります。Plan モードで決定し、範囲を限定した実装を Autopilot に任せます。

## 背景

AI コーディング エージェントを開発フローに導入しても、基本は変わりません。むしろ、基本を守ることが一層重要になります。多くの開発者は、次のような流れで作業します。

1. 作業内容を記述した issue を登録します。
2. 実装する内容を計画します。
3. コードを作成してレビューします。
4. テストを実行してコードを検証します。
5. 新機能を手動で検証します。
6. プル リクエスト (PR) を作成します。
7. コードレビューと継続的インテグレーションが成功したら、コードをマージします。

> [!NOTE]
> 詳細な進め方はチームや組織によって異なりますが、多くは上記の流れを基本にしています。

この標準的な手順に沿うことで、AI が生成したコードが要件を満たし、手作業で書いたコードと同じレビュー プロセスを経るようにできます。

## 会話モード

**会話モード**は、エージェントにどの程度の自律性を与えるかを制御します。<kbd>Shift</kbd>+<kbd>Tab</kbd> を押すとモードを切り替えられます。

- **Interactive**: エージェントと一緒に作業します。エージェントは変更を提案し、次に進む前に入力を待ちます。
- **Plan**: エージェントが先に計画を作成します。プロジェクト ファイルの編集はできません。
- **Autopilot**: エージェントがコードの作成、テストの実行、反復を自律的に行い、タスクの完了を目指します。

まず Plan モードで計画を確認し、その後 Autopilot で実装します。

## issue から始める

絞り込みの作業を始める前に、Codespace に戻り、リポジトリとターミナルの準備ができていることを確認します。

1. Codespace に戻ります。停止している場合は再起動します。
2. 星評価の PR がマージ済みであることを確認します。
3. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
4. `main` を更新し、絞り込み作業用のブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を 2 回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての issue を表示します。
8. 矢印キーで **Allow users to filter games by category and publisher** というタイトルの issue を選択します。
9. <kbd>C</kbd> を押して issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトの先頭に `#7` (または同様の番号) が表示されます。`#` を使うと、GitHub の issue やプル リクエスト (PR) をコンテキストに含められます。

## 絞り込み機能を計画する

計画を立てると、Copilot に作業を任せる前に機能の実装方針やタスクの進め方を決められます。複雑な作業では、事前に計画することをお勧めします。Plan モードに切り替えて、Copilot に計画の作成を依頼します。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替えます。プロンプトの下に **Plan** と表示されていることを確認します。
2. 前の手順で追加した issue の後に、次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot はプロジェクトを調査し、最適な方法を検討して計画を作ります。

3. 絞り込みの動作について質問されたら、希望に基づいて回答します。どの回答が正しいということはありません。
4. 計画が完成したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して計画を展開します。
5. 計画を上から下まで確認します。
6. 決定した内容と合わない部分があれば、Copilot に修正を依頼します。

## Autopilot を承認する

計画を作成してレビューできたら、実装に進みます。Autopilot を使って Copilot に作業を任せます。

Autopilot では、Copilot が完了したと判断するまで問題に取り組み、反復できます。

1. **Accept plan and build on autopilot (recommended)** (またはインストール済みバージョンで同様の名前の項目) を選択します。
2. プロンプトの下に **Autopilot** と表示されていることを確認します。
3. Copilot が計画に沿って反復し、コードを生成してテストを実行する様子を確認します。

> [!NOTE]
> 承認すると、すぐに実装が始まることがあります。必ず計画を先に確認してください。依存関係が不足している、またはポートが競合していると Copilot が報告した場合は、チェック完了と判断する前にセットアップの問題を解決します。

## 実装をレビューして検証する

コードを生成した後、ほかのコードと同様にマージ前にレビューします。コードを確認し、サイトを起動して正しく動作することを確かめましょう。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードに切り替えます。モード表示に **Plan** や **Autopilot** がないことを確認します。
2. `/diff` を実行し、絞り込み機能とテストを確認します。
3. 結果を issue と計画時の決定に照らし合わせます。
4. コードのレビューが終わったら <kbd>Esc</kbd> を押して差分表示を閉じます。
5. プロジェクトのチェック結果を確認し、失敗があれば Copilot に解決を依頼します。

## 新しい機能を試す

コードは問題なさそうですが、実際に動くでしょうか。前回と同じようにアプリを起動し、Codespaces のポート転送を通じてサイトを開きます。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能になったら、**ブラウザーで開く**を選択します。
3. 計画で決めたカテゴリ、販売元、組み合わせによる絞り込みを試します。
4. リセットと該当結果がない場合の動作が、issue と決定した内容に合っていることを確認します。
5. Codespace に戻り、Copilot に起動した開発サーバーを停止するよう依頼します。

## まとめと次のステップ

会話モードを切り替えて機能を実装し、レビューできました。このレッスンでは、次の操作を行いました。

- GitHub issue から新しい Copilot の会話を開始しました。
- Plan モードで要件を定義しました。
- Autopilot モードで新機能を実装しました。
- コードをレビューしました。
- 転送されたブラウザーで手動検証しました。

次は、コードが文書化された慣例に沿うように、[カスタム指示を使います][next-lesson]。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンド リファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
