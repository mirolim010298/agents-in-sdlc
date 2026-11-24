---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

未解決のセキュリティ問題、更新が必要なレガシー コード、バックログに残った機能要求など、技術的負債に悩む組織は少なくありません。GitHub Copilot の cloud agent は、コードの更新や機能追加などのタスクを自律的に実行します。完了すると、人間がレビューできるドラフト PR を作成します。時間のかかる作業を任せることで、開発者はより大きな課題に集中できます。

Copilot cloud agent で次の内容を学びます。

- コード生成環境をカスタマイズする方法。
- 操作を安全に行う方法。
- 範囲を明確に定めた issue の重要性。
- issue を Copilot に割り当てる方法。

## シナリオ

Tailspin Toys には解消したい技術的負債があります。最初のサイトを開発した委託先は、ドキュメントをほとんど残しませんでした。まず、アプリケーションのエクスポート関数すべてに TSDoc のドキュメント コメントを追加します。

さらに、デザイン チームはゲームを見つけやすくしたいと考えています。ゲーム詳細ページに同じカテゴリのほかのゲームを表示し、閲覧を続けられるようにします。現時点では完成された実装は不要で、UX の受け入れテストに使える状態を目指します。この作業はブロッカーですが、優先度の高い issue がほかにあります。

どちらも、優先順位が下がりやすいタスクです。Copilot cloud agent に割り当てると、非同期で作業させながら別のタスクに取り組み、後で結果をレビューできます。

## GitHub Copilot cloud agent を使う

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者と同じようにバックグラウンドでタスクを実行します。[GitHub issue を Copilot に割り当てる](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)方法などがあります。割り当てると、Copilot は進捗を追跡するドラフト プル リクエストを作成し、環境を設定して作業を始めます。作業中または完了後にセッションを確認できます。解決案をレビューする準備ができると、プル リクエストで通知されます。

## 範囲を明確にした指示の重要性

GitHub Copilot に魔法はありません。考える作業を省略できるわけではありません。一見簡単な操作でも、詳しく調べると複雑なことがあります。[Copilot cloud agent に依頼するタスクの範囲][cloud-agent-best-practices]を慎重に決めてください。AI ペア プログラマーとして扱い、段階を踏んで学び、試し、調整します。生成 AI を導入しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示が Copilot を導く仕組みを確認しました。まだ `.github/copilot-instructions.md` を見ていない場合は、cloud agent に作業を割り当てる前に、リポジトリに含まれる指示ファイルを読み取り専用で確認してください。後で結果への影響を確認できます。

- `.github/copilot-instructions.md` の **Code standards** セクションで、TypeScript の慣例と TSDoc コメントの要件を確認します。
- `.github/instructions/unit-tests.instructions.md` の `applyTo` フロントマターで、`**/*.test.ts` に指示が適用されることを確認します。

次のセクションで `Code lacks documentation` issue を cloud agent に割り当てると、結果のプル リクエストに TSDoc コメント、TypeScript の慣例、ファイル ヘッダーが反映されます。これらの指示ファイルの内容は後の演習で PR をレビューするときに確認します。

## Copilot cloud agent の開発環境を設定する

コードの作成には、通常、必要なツールを用意して環境を整える作業が必要です。Copilot にタスクを割り当てる場合も同様で、cloud agent も SWE と同じように作業します。

cloud agent は作業環境に [GitHub Actions][github-actions] を使います。`.github/workflows/copilot-setup-steps.yml` に[セットアップ ワークフロー][setup-workflow]を作成すると、作業開始前に必要な開発ツールや依存関係をインストールできます。ラボの流れを簡単にし、学習機会を提供するため、この環境は事前に設定されています。Node.js、プロジェクトの依存関係、エンドツーエンド テスト用のブラウザー、単一 Astro アプリ用にマイグレーションとシードを適用した SQLite データベースを用意します。

```yaml
name: "Copilot Setup Steps"

# リポジトリの "Actions" タブからセットアップ手順をテストできます
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # *手順*に必要な最小限の権限を設定します。Copilot は操作用に独自のトークンを受け取ります。
    permissions:
      # 依存関係のインストールなど、セットアップ手順でリポジトリをクローンする場合は `contents: read` 権限が必要です。クローンしない場合は、手順の完了後に Copilot が自動で実行します。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体は Astro + Drizzle/libSQL です)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ビルドとテストでデータを使えるように、ローカル SQLite データベースをマイグレーションしてシードします。
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub Actions ワークフローに似ていますが、重要な点があります。

- `copilot-setup-steps` というジョブが 1 つあります。このジョブは Copilot がプル リクエストに取り組む前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーがあり、リポジトリの **Actions** タブから手動で実行できます。Copilot の実行を待たずにワークフローが成功するか確認できます。

## ドキュメントを追加する

ドキュメントの重要性は広く認識されていますが、古くなっていたり不足していたりするプロジェクトは少なくありません。このような技術的負債は放置されやすく、作業効率を下げ、コードベースの保守や新しい開発者の参加を難しくします。Copilot はドキュメントの作成を得意とするため、cloud agent に依頼するのに適したタスクです。作業中はバックグラウンドで必要なドキュメントを作成し、後の演習で結果をレビューします。

1. 新しいブラウザー タブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択します。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次を入力します。

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して割り当てダイアログを開きます。

   ![issue への Copilot の割り当て](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. `[WIP]: Code lacks documentation` のようなタイトルのプル リクエスト (PR) を開きます。一覧に表示されない場合は少し待ち、ブラウザーを更新します。
12. 数分後、Copilot が PR に todo リストを作成します。

> [!NOTE]
> Copilot が todo リストを PR に追加するまで数分かかる場合があります。前述のワークフローで環境を作り、プロジェクトを分析して、最適な方法を決めています。

13. リストと、実行予定のタスクを確認します。
14. プル リクエストのタイムラインを下にスクロールし、Copilot が issue の作業を始めたことを示す更新を確認します。
15. **View session** ボタンを選択します。

   ![Copilot セッションの表示](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 更新された状態が表示されない場合は、ウィンドウを更新してください。

16. ライブ セッションをスクロールし、Copilot がコードを調査して状態を把握し、計画を検討してコードを作成する様子を確認します。

この作業には数分かかります。Copilot cloud agent の主な目的は、作業を非同期で実行し、開発者が別のタスクに集中できるようにすることです。別のタスクも Copilot cloud agent に割り当て、並行してアプリケーションに機能を追加しましょう。

## ゲーム詳細ページに関連ゲームを追加する

cloud agent の利点の 1 つは、作業を分けられることです。デザイン チーム向けに関連ゲームを追加する作業が短時間でも、別の作業に時間を使えます。cloud agent に割り当てましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択します。
4. **Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次を入力します。

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して割り当てダイアログを開きます。

   ![issue への Copilot の割り当て](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

最初のコメントに 👀 が表示され、Copilot が作業を始めたことを示します。

![Copilot が issue に取り組んでいることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼にも取り組み始めます。SWE と同様に作業するため、積極的に監視する必要はありません。完了後にレビューします。次はカスタム エージェントの作成と使用を確認します。

## まとめと次のステップ

[GitHub Copilot cloud agent][copilot-agents] を学びました。cloud agent に issue を割り当てて、非同期で処理させることができます。技術的負債への対応、新機能の作成、フレームワーク間のコード移行などに使えます。

このレッスンでは、次の操作を行いました。

- コード生成環境をカスタマイズしました。
- 操作を安全に行う方法を確認しました。
- 範囲を明確に定めた issue の重要性を学びました。
- issue を Copilot に割り当てました。

cloud agent がバックグラウンドで作業している間に、カスタム エージェントの作成と使用に進みます。[Copilot cloud agent は MCP サーバーも利用でき][cloud-agent-mcp]、前のモジュールで確認したカスタム指示も使います。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタム エージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
