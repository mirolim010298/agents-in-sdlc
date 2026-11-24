---
title: "演習 2 - Copilot エージェント モードで機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリケーションの小さな更新でも、複数のファイルを修正したり、テストを実行したりする必要があります。開発者は必要なファイルを見つけ、変更し、テストを実行し、デバッグし、変更し忘れたファイルを探して、さらに更新することがあります。

こうした作業に役立つのが Copilot エージェント モードです。

Copilot エージェント モードは IDE 内でより自律的に作業するよう設計されています。開発者と同様に既存のプロジェクト構成を調査し、必要な更新を行い、テストなどのタスクを実行し、見つかった問題を自動的に修正します。エージェント モードでサイトに新しい機能を追加する方法を確認しましょう。

> [!NOTE]
> 名前は似ていますが、エージェント モードと cloud agent は異なる用途向けです。エージェント モードは IDE 内で作業し、短いフィードバック サイクルと対話を可能にします。cloud agent はチームのメンバーのように非同期で作業し、issue とプル リクエストを通じてやりとりします。

この演習では、次の操作を学びます。

- Copilot エージェント モードがプロジェクトを調査し、関連ファイルを見つけて、複数ファイルにまたがる変更を行う方法。
- GitHub Copilot エージェント モードで UI とデータ レイヤーを更新し、新機能を実装する方法。
- コードベースにマージする前に、Copilot エージェント モードが生成した変更とテストをレビューする方法。

## シナリオ

ゲーム一覧が増えているため、ユーザーがカテゴリや販売元で絞り込めるようにします。前の演習では販売元ヘルパーを追加しました。今回は Copilot エージェント モードを使い、残りのデータ レイヤー、UI、テストを完成させます。

## Tailspin Toys Web サイトを実行する

変更を加える前に、現在の機能を理解するため Tailspin Toys の Web サイトを確認します。

このサイトは開発者をテーマにしたボードゲームのクラウドファンディング プラットフォームです。ゲーム一覧と詳細を表示します。単一の Astro アプリで、ビルド時に静的 HTML を生成します。ページは Drizzle ORM を使い、フロントマターからローカル SQLite データベースを直接照会します。別のバックエンド API やクライアント側 UI フレームワークはありません。再利用可能なデータ アクセス ヘルパーは `src/lib/` に置き、操作性は標準 DOM API を使う小さな Astro `<script>` で追加します。

### Web サイトを起動する

サイトを簡単に実行できるよう、単一の Astro 開発サーバーを起動する `npm run dev` タスクがあります。GitHub Codespace で次の手順を実行します。

1. Codespace に戻ります。前の演習の後で `main` に戻っているはずです。
2. <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押して Codespace で新しいターミナルを開きます。
3. 絞り込み用のブランチを作成して切り替えます。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドを実行して Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro 開発サーバーの準備ができると、次のような URL が表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` を開くよう促すダイアログが表示された場合は、**x** を選択して閉じます。

5. <kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら、ターミナルに表示された `http://localhost:4321` のリンクを選択し、Web サイトを開きます。

> [!NOTE]
> Codespace のターミナルで localhost URL のリンクを選択すると、自動的に `https://<your-codespace-name>-4321.app.github.dev/` に転送されます。これは Codespace で実行している Web サーバーへのプライベート トンネルです。

### Web サイトを確認する

サイトが起動したら、機能を確認します。主な機能は次のとおりです。

- **ホーム ページ**: ボードゲームの一覧を、タイトル、画像、説明とともに表示します。
- **ゲーム詳細ページ**: ゲームを選択すると、タイトル、説明、販売元、カテゴリなどの情報を表示します。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> 次の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。モードとモデルの選択は演習ごとに異なり、必要な場合は手順で説明します。

Web サイトの初期実装は動作しますが、機能を改善したいと考えています。まずバックログを確認します。テンプレートからプロジェクトをセットアップすると issue のバックログが自動で作成されるため、GitHub Copilot に内容を表示させます。

1. Chat ビューのエージェント ドロップダウンから **Agent** を選択します。**Agent** は複数ファイルにまたがる変更を計画・実装し、ターミナル コマンドを実行してツールを呼び出します。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデルの一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> ワークショップの作成者が特定のモデルを推奨する意図はありません。ワークショップでは Claude Sonnet 4.5 を使ったため、手順に含めています。コード提案の一貫性を高めることが目的ですが、LLM は確率的に動作するため、手順と異なる提案が表示されることがあります。これは正常な動作です。

> [!NOTE]
> 確率的な動作のため、Copilot が異なる MCP コマンドを使う場合がありますが、タスクは完了できるはずです。

3. 次のプロンプトを Copilot に送り、issue のバックログを確認します。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. **Continue** を選択して、すべての issue を一覧表示するコマンドを実行します。
5. 生成された issue の一覧を確認します。

Copilot がユーザーに最も役立つと思われる項目を優先順位付けしたことを確認します。

## 指示ファイルを確認する

Copilot にコードを生成させる前に、作業のコンテキストを与える指示ファイルを確認します。サイトの機能追加方法に関する情報を含む [ユーザー インターフェイス (UI)][ui-instructions] ファイルを使います。

1. Codespace で `.github/instructions/ui.instructions.md` を開きます。
2. 機能追加のガイダンスを確認します。次の内容が含まれます。
   - アーキテクチャの概要。
   - コンポーネント設計、テスト可能性、アクセシビリティの原則。
   - Astro、Tailwind CSS、Drizzle などのファイル別指示へのリンク。

> [!TIP]
> 指示ファイルから別の指示ファイルやプロジェクト ファイルを参照できます。パスは指示ファイルからの相対パスです。指示を再利用し、大きな内容を管理しやすい小さな単位に分け、例やテンプレートを示せます。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md

## 絞り込み機能を実装する

絞り込み機能を完成させるには、少なくとも次の 3 つを更新します。

- データ レイヤー (`src/lib/`) の絞り込みロジックを追加または改善します。
- 絞り込み動作のテストを追加または更新します。
- ゲーム一覧ページに絞り込み UI を追加します。

さらに、コードベースにマージする前にテストが成功する必要があります。Copilot エージェント モードにこの作業を依頼します。

1. 現在の Copilot 会話を続けるか、**New Chat** を選択して新しい会話を始めます。
2. **Add Context**、**Instructions**、**ui** を選択して指示ファイルを追加します。

   ![UI 指示ファイルを選択する例](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェント ドロップダウンで **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

4. モデルが **Claude Sonnet 4.5** のままであることを確認します。
5. バックログの関連 issue に基づいて機能を実装するよう、次のプロンプトを送ります。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調査し、データ レイヤー、UI、テストのファイルを見つけて変更し、テストを実行する様子を確認します。

   ![Copilot がプロジェクト ファイルを調査する画面](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトの調査、ファイルの変更、テストなどを実行するため、数分かかることがあります。作業中、コード エディターに **Keep** と **Undo** が表示される場合があります。すべての変更に対する **Keep** または **Undo** は完了後に選択できるため、作業中に選ぶ必要はありません。

7. Copilot から求められたら **Continue** を選択してテストを実行します。

   ![Copilot Chat ペインでテスト実行の確認を求めるダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に一時停止したり、テストが失敗したりすることがあります。問題ありません。Copilot はコード生成とテストを繰り返し、エラーが見つからなくなるまで進めます。

   ![Copilot エージェント モードの完了した Chat セッション](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot などの AI ツールが生成したコードは、必ずレビューしてください。

10. Web サイトを起動したブラウザーに戻り、新しい機能を確認します。
11. 動作とコードを確認したら、Copilot Chat ウィンドウで **Keep** を選択します。

## まとめと次のステップ

GitHub Copilot エージェント モードで Tailspin Toys に機能を追加する方法を学びました。

- GitHub Copilot エージェント モードで UI とデータ レイヤーを更新し、新機能を実装しました。
- Copilot エージェント モードでプロジェクトを調査し、関連ファイルを見つけ、複数ファイルにわたって変更しました。
- コードベースにマージする前に、Copilot エージェント モードが生成した変更とテストをレビューしました。

次は[Playwright MCP サーバーで機能をテストし][next-lesson]、プル リクエストを作成します。

### 追加の演習 — ページネーションを実装する

ゲーム一覧が増えるとページネーションが必要になります。この演習で学んだことを使い、Copilot にページネーションを実装するよう依頼します。

- 既存の指示ファイルを使うなど、既存のベスト プラクティスに従います。
- ページ サイズをユーザーが選べるようにするか、固定にするかなど、実装方法を検討します。
- 希望どおりの実装に必要なガイダンスをプロンプトに含めます。
- Copilot に変更やコンテキストを伝え、反復が必要な場合があります。これは Copilot を使う通常のワークフローです。

## リソース

- [Copilot の Ask、Edit、Agent モード: それぞれの違いと使い分け][choose-mode]
- [VS Code のエージェント モード][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
