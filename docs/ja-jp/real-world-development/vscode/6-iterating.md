---
title: "演習 6 - GitHub Copilot の作業を反復する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
next: false
---

| [← 前のレッスン: エージェントの監視と管理][previous-lesson] |
| :-- |

## 作業をレビューする

このラボでは、ユーザー エクスペリエンスを改善する複数の作業で GitHub Copilot を使いました。エージェント モードでクライアントとサーバーにまたがる絞り込み機能を追加し、Playwright MCP サーバーでブラウザーから動作を確認し、カスタム エージェントでハイ コントラストとライト モードの切り替えなどのアクセシビリティ機能を実装しました。さらに、作業中にセッションへ指示を追加しました。ローカルの変更を公開し、チームと同じ手順でレビューしましょう。

### シナリオ

生成 AI を導入しても、ソフトウェア設計と DevOps の基本は変わりません。Copilot が作成したものも通常のレビューを行います。Codespace からアクセシビリティの変更をプッシュし、プル リクエストを作成して、チームにレビューを依頼する前に差分を確認しましょう。

## アクセシビリティ機能を公開する

[演習 4][exercise-4] と[演習 5][exercise-5]でアクセシビリティ カスタム エージェントを使って実装したハイ コントラストとライト モードの切り替えは、Codespace にコミット済みの変更として保存されています。ブランチにプッシュしてプル リクエストを作成し、チームにレビューしてもらいます。

1. Codespace に戻ります。
2. VS Code で **Source Control** ビューを開きます。
3. アクセシビリティの変更がコミット済みであることを確認します。演習 5 から未コミットの変更がある場合は、`Add high-contrast and light-mode toggles` のようなわかりやすいメッセージでステージしてコミットします。
4. **Publish Branch** を選択してブランチを公開します。または **...** メニューから **Push** を選択します。
5. VS Code が github.com で新しいブランチを開くことを提案します。案内に従うか、リポジトリを開いてブランチのバナーにある **Compare & pull request** を選択します。
6. 明確なタイトル (例: `Add high-contrast and light-mode toggles`) と、実装内容および理由を簡潔に説明する説明を入力します。
7. **Create pull request** を選択します。
8. PR を開いたら **Files changed** タブを選び、作業全体をレビューします。次の点を確認します。
   - モードを切り替える UI コンポーネント。
   - ユーザー設定を保存する local storage の使用。
   - ハイ コントラストとライト モードの CSS またはスタイルの変更。
   - ARIA ラベル、キーボード操作などのアクセシビリティ属性。
   - モード切り替えを管理する JavaScript/TypeScript コード。

9. **Conversation** タブに戻ります。
10. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する](../../../_images/shared-approve-workflows.png)

11. ワークフローの完了を待ち、すべて成功したことを確認します。

> [!TIP]
> アクセシビリティ作業に別の視点が必要な場合は、PR のコメントで `@copilot` に「この PR に追加の WCAG の問題がないかレビューしてください」や「キーボード操作の改善案を提案してください」のように依頼します。Copilot はコメントに対応する新しいセッションを開始します。

## 任意の演習 — ローカルで試す

IDE でエージェントと反復して作業するスキルは、実践を通じて身につきます。VS Code で次のような追加セッションを試してください。

- ゲーム詳細ページに支援者向け問い合わせフォームを追加する。
- ゲーム一覧ページにページネーションを実装する。
- `src/lib/` のデータ アクセス ヘルパーに入力検証とエラー処理を追加する。
- アクセシビリティ エージェントの対象を広げ、サイト全体のキーボード フォーカス順序を監査する。

## まとめ

VS Code ハーネスを完了しました。このラボでは、次の操作を行いました。

- **Playwright MCP で機能を手動テストしました。** Playwright MCP サーバーを追加し、Copilot にブラウザーを操作させて、プル リクエストを作成する前に絞り込み機能を確認しました。
- **エージェント モードで複数レイヤーにまたがる変更を行いました。** 1 つのセッションでクライアント、サーバー、テストにまたがる絞り込み機能を追加しました。
- **カスタム エージェントを使いました。** エージェント ピッカーからアクセシビリティ エージェントを選び、リポジトリのアクセシビリティ機能を実装する様子を確認しました。
- **エージェント セッションを管理して指示しました。** 提案された変更をインラインでレビューし、必要なものを採用し、ライト モードの追加プロンプトでセッションを拡張しました。
- **プル リクエストで変更をレビューしました。** ローカルの作業を公開し、チームと同じ方法で最初から最後まで確認しました。

## レビューと次のステップ

VS Code ハーネスの必須部分は完了です。ここでワークショップを終了できます。

Copilot のエージェント機能を別の視点から学ぶ場合は、次のハーネスをご覧ください。

- 💻 **[CLI ハーネス](../../cli/)** — Plan と Autopilot モード、スキル、QA カスタム エージェント、Playwright MCP、Agent Merge、コンテキストを使った引き継ぎを利用し、ターミナルからレビュー済みの変更を 2 つリリースします。
- ☁️ **[Cloud agent ハーネス](../../cloud/)** — cloud agent への issue 割り当て、エージェント ページでのセッション監視、プル リクエストの非同期レビューを学びます。

この演習の続きとして、[awesome-copilot][awesome-copilot] から自分のプロジェクトに合わせた指示ファイル、カスタム エージェント、スキルを探すこともできます。

任意の拡張として、[任意: Foundry を取り入れる][exercise-7]では、VS Code と Microsoft Foundry Toolkit でモデルを準備し、Backer Concierge をデプロイしてサイトに接続します。

## リソース

- [GitHub Copilot][github-copilot]
- [VS Code の Copilot Chat][copilot-chat-vscode]
- [エージェント モードを使う][agent-mode]

---

| [← 前のレッスン: エージェントの監視と管理][previous-lesson] |
|:--|

[previous-lesson]: ../5-managing-agents/
[exercise-4]: ../4-custom-agents/
[exercise-5]: ../5-managing-agents/
[exercise-7]: ../7-foundry-toolkit/
[github-copilot]: https://github.com/features/copilot
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
[awesome-copilot]: https://github.com/github/awesome-copilot
