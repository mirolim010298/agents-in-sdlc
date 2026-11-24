---
title: "演習 5: GitHub Copilot の作業を反復する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このラボでは、ユーザー エクスペリエンスを改善して機能を追加する複数のタスクで GitHub Copilot を使いました。コードへのドキュメント追加、デザイン チームが改善できる関連ゲーム機能の作成、ハイ コントラストとライト モードの切り替えを含むアクセシビリティ機能を依頼しました。コードの変更を確認し、必要に応じて Copilot にフィードバックを伝え、作業を改善します。

### シナリオ

生成 AI を導入しても、ソフトウェア設計と DevOps の基本は変わりません。生成されたコードをレビューし、通常の DevOps プロセスに沿って進めます。チーム全員にレビューを依頼する前に、Copilot が作成したドキュメント、関連ゲーム機能、アクセシビリティ機能を確認しましょう。

## セキュリティと GitHub Copilot cloud agent

Copilot cloud agent は監督者なしで非同期にタスクを実行するため、安全性を維持するセキュリティ制約があります。

- Copilot はリポジトリへの読み取りアクセスのみを持ち、書き込みできるのは作業に使うブランチだけです。
- cloud agent は GitHub Actions 内に一時的な専用環境を作成して実行されます。
- GitHub Actions ワークフローを実行するには、人間の承認が必要です。
- 既定では [外部リソースへのアクセス][agent-firewall]が制限されており、MCP サーバーへのアクセスも制限されます。

## 生成されたドキュメントをレビューする

最初のプル リクエスト (PR) である、コードへのドキュメント追加をレビューします。GitHub.com の標準的な PR インターフェイスを使います。

> [!NOTE]
> PR に GitHub Copilot がファイアウォールでブロックされたという警告が表示される場合があります。Copilot は外部 MCP サーバーへの呼び出しを含む外部リソースへのアクセスが既定で制限されているため、これは**想定どおり**です。必要に応じて [cloud agent のファイアウォールを構成または無効化][agent-firewall]できます。

1. github.com のリポジトリに戻ります。
2. **Pull Requests** を選択して PR の一覧を開きます。
3. **Add missing documentation** などのタイトルのプル リクエストを開きます。

> [!NOTE]
> Copilot がまだ作業中の場合、PR に **[WIP]** の表示があります。作業が完了するまで待ちます。数分かかることがあります。その間に休憩したり、学んだことを振り返ったりしてください。

4. 準備ができたら **Files changed** タブを選び、変更をレビューします。

   ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. TSDoc のドキュメント コメントなど、新たに更新されたコードとドキュメントを確認します。具体的な変更は状況によって異なります。演習 2 の開始時に確認したカスタム指示ファイルによる TSDoc コメント、TypeScript の慣例、ファイル ヘッダーを確認してください。
6. 問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローが承認待ちであることを示す表示を探します。
8. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する](../../../_images/shared-approve-workflows.png)

9. PR の checks セクションにワークフローがキューに入ります。問題がなければ、単一 Astro アプリのプロジェクト チェックが成功します。完了まで数分かかる場合があります。

## GitHub Copilot に変更を依頼する

プル リクエストで Copilot と作業するのは一方通行ではありません。チーム メンバーと同じように、PR のコメントやコードの行内コメントで Copilot にメンションできます。Copilot はコメントを認識し、修正のためのセッションを開始します。結果は確定的ではないため、必ずしも適切な依頼内容を指定できるわけではありません。次のような変更を依頼できます。

- 各コード ファイルの先頭に、内容を簡潔に説明するコメント ヘッダーを追加する。
- TypeScript と Astro のファイルに TSDoc のドキュメント コメントを追加する。
- Astro アプリの構成を説明する README を作成する。

1. **@copilot** をメンションして、生成されたドキュメントの変更を依頼するコメントを追加します。上記の例から選ぶか、コードベースのドキュメントに関する別の変更を依頼します。
2. **View Session** を選択し、Copilot が作業する様子を確認します。更新のために新しいセッションが始まります。
3. **Back to pull request** を選択すると PR に戻れます。

   ![プル リクエストに戻る](../../../_images/ex7-back-to-pr.png)

4. Copilot の変更が終わると、PR に新しいコミットが表示されます。
5. **Files changed** タブを選択し、変更をレビューします。

満足するまで反復できます。問題がなければ、ドラフト PR をレビュー可能な状態に変更して `main` ブランチへマージします。

![PR をレビュー可能な状態に変更する](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

ゲーム詳細ページに関連ゲームを表示する issue を解決するため、Copilot が作成した PR を確認します。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Show related games on the game details page** などのタイトルの PR を選択します。
4. **Files changed** タブを選び、生成されたコードをレビューします。
5. 問題がなければ **Conversation** タブに戻り、下にスクロールします。
6. ワークフローが承認待ちであることを確認します。
7. 承認待ちの場合は **Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する](../../../_images/shared-approve-workflows.png)

8. PR の checks セクションにワークフローがキューに入り、単一 Astro アプリのチェックが完了するまで待ちます。
9. **任意:** Codespace でこのブランチに切り替えて、関連ゲーム機能を手動でテストできます。Copilot が作成したブランチ名 (例: **copilot/fix-8**) を `<branch-name>` に置き換えて、Codespace のターミナルで次を実行します。

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot が関連ゲーム機能を作成しました。前と同じように、cloud agent と反復して変更を依頼できます。たとえば関連ゲームの表示件数を変えたり、作業がカスタム指示を追加する前に割り当てられたものであることを踏まえて、コメント ヘッダーや TSDoc コメントを追加したりできます。**Conversation** タブにコメントを追加すると、Copilot が新しいセッションを開始します。

## アクセシビリティ機能をレビューする

最後に、アクセシビリティ カスタム エージェントで実装した機能を確認します。この PR には演習 3 で依頼したハイ コントラスト モードと、演習 4 の Mission control から追加したライト モードが含まれます。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Add high contrast mode to website** などのタイトルの PR を選択します。

> [!NOTE]
> Copilot がまだ作業中の場合、PR に **[WIP]** の表示があります。作業が終わるまで待ちます。数分かかる場合があります。

4. **Files changed** タブで生成されたコードをレビューします。
5. 次の項目に特に注意して、実装を確認します。
   - モードを切り替える UI コンポーネント。
   - ユーザー設定を保存する local storage の使用。
   - ハイ コントラストとライト モードの CSS またはスタイルの変更。
   - ARIA ラベル、キーボード操作などのアクセシビリティ属性。
   - モード切り替えを管理する JavaScript/TypeScript コード。

6. 問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローが承認待ちであることを示す表示を確認します。
8. 承認待ちの場合は **Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する](../../../_images/shared-approve-workflows.png)

9. PR の checks セクションでワークフローが完了し、すべて成功することを確認します。
10. **任意:** Codespace でこのブランチに切り替え、アクセシビリティ機能を手動でテストできます。Copilot が作成したブランチ名を `<branch-name>` に置き換えて、次を実行します。

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

   アプリケーションを起動し、ハイ コントラストとライト モードの切り替えをブラウザーで試します。ページを再読み込みしても設定が保持されることを確認します。

アクセシビリティ エージェントによって、Copilot はアクセシビリティのベスト プラクティスに従って機能を実装できました。アクセシビリティに懸念や改善点があれば、前の PR と同様にコメントで **@copilot** に更新を依頼します。

## 任意の演習 — 委任を続ける

cloud agent は、バックログの実際のタスクを任せて別の作業に集中するときに役立ちます。いくつか issue を作成し、Copilot に割り当ててみてください。

- ゲーム詳細ページに支援者向け問い合わせフォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データ アクセス ヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent ハーネスを完了しました。次の内容を学びました。

- **リポジトリに含まれるカスタム指示ファイルを確認し、** cloud agent の結果への影響を確認しました。
- **issue を Copilot cloud agent に割り当て、** 環境の準備、計画、非同期の実行を確認しました。
- **カスタム エージェントを作成・使用し、** ハイ コントラストとライト モードの切り替えを追加しました。
- **Copilot agents ページを Mission control として使い、** 実行中のアクセシビリティ セッションを監視して案内しました。
- **cloud agent のプル リクエストをレビューして反復し、** `@copilot` に変更を依頼してワークフローを承認しました。

## レビューと次のステップ

Cloud agent ハーネスはこれで完了です。ほかのハーネスでは、異なる環境から関連するシナリオを学べます。

- 🖥️ **[VS Code ハーネス](../../vscode/)** — IDE から Copilot Chat のエージェント モードと MCP 統合を試します。
- 💻 **[CLI ハーネス](../../cli/)** — Plan と Autopilot モード、エージェント スキル、QA カスタム エージェント、Playwright MCP、Agent Merge、cloud agent への任意の `/delegate` を使い、レビュー済みの変更を 2 つターミナルからリリースします。

自分のリポジトリでは、次のような作業も試せます。

- リファクタリングやテスト カバレッジの issue を cloud agent に割り当てます。
- 別の分野のカスタム エージェントを作成します。
- 異なる技術スタック向けに `copilot-setup-steps.yml` を設定します。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot agents について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]
- [Copilot cloud agent のファイアウォールを構成する][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
