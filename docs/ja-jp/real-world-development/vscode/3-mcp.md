---
title: "演習 3 - Playwright MCP サーバーで機能をテストする"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: エージェント モード][previous-lesson] · [次のレッスン: カスタム エージェント →][next-lesson]

エージェント モードで絞り込み機能を作成しました。プル リクエストを開く前に、ブラウザーで正しく動作するか確認します。自分でアプリを操作する代わりに、**Playwright MCP サーバー**を接続し、Copilot に実際のブラウザーで機能をテストさせます。その後、ブランチを公開して PR を作成します。

この演習では、次の操作を行います。

- Model Context Protocol (MCP) と MCP サーバーが Copilot にツールを追加する仕組みを学びます。
- Playwright MCP サーバーをワークスペースに追加します。
- ブラウザーで絞り込み機能を手動テストするため、Copilot に Playwright の使用を依頼します。
- ブランチを公開し、絞り込み作業のプル リクエストを作成します。

## Model Context Protocol (MCP) とは

エージェント モードはエディターの外部にアクセスできると、さらに便利になります。Copilot がそれを実現する方法が Model Context Protocol (MCP) です。エージェントが外部のツールやサービスと通信するための標準です。

![エージェント モードとコンテキスト、LLM、MCP サーバーや VS Code 拡張機能が提供するツールの関係を示す図](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) は、AI エージェントが外部ツールやサービスと通信する仕組みを提供します。MCP を使うと、エージェントはリソースを使って最新情報にアクセスしたり、ツールを使って依頼に応じた操作を実行したりできます。

ツールやリソースには、AI エージェントと外部サービスの橋渡しをする MCP サーバーを通じてアクセスします。MCP サーバーは、既存 API や npm パッケージなどのローカル ツールとの通信を管理します。各サーバーはエージェントが利用できるツールとリソースを提供します。

広く使われている MCP サーバーには、次のものがあります。

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**: GitHub リポジトリ、issue、プル リクエストを管理する API にアクセスできます。リポジトリの作成や更新、issue やプル リクエストの管理などを実行できます。
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)**: Playwright を使ったブラウザー自動化機能を提供します。Web ページの移動、フォームの入力、ボタンの選択などを行えます。

ほかにもさまざまなツールやリソースにアクセスできる MCP サーバーがあります。GitHub は、エコシステム内のサーバーを見つけやすくし、コントリビューションを促すために [MCP レジストリ](https://github.com/mcp)をホストしています。

> [!CAUTION]
> セキュリティ面では、MCP サーバーをプロジェクト内のほかの依存関係と同様に扱ってください。利用前にソース コードをよく確認し、発行元を検証し、セキュリティへの影響を検討します。信頼できる MCP サーバーだけを使い、機密リソースや操作へのアクセス許可に注意してください。

## MCP の構成を確認する

`.vscode/mcp.json` ファイルで、この VS Code ワークスペースで利用する MCP サーバーを設定します。

1. Codespace で `.vscode/mcp.json` を開きます。
2. `github` サーバーがすでに設定されています。

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

この `github` エントリはプロジェクト テンプレートに含まれているため、前の演習で Copilot は issue のバックログを読み取れました。[リモート GitHub MCP サーバー][remote-github-mcp-server]を使うため、ローカルへのインストールは不要です。VS Code は HTTP で接続し、Copilot がツールを初めて使うときに GitHub で認証します。

## Playwright MCP サーバーを追加する

2 つ目のサーバーを追加します。[Playwright MCP サーバー][playwright-mcp-server]を使うと、Copilot がブラウザーを操作できるため、機能をテストできます。

1. `.vscode/mcp.json` に `github` と並べて `playwright` エントリを追加し、ファイルが次のようになるようにします。

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. ファイルを保存します。

リモートの `github` サーバーと異なり、`playwright` はローカル サーバーです。VS Code は `npx @playwright/mcp@latest` を実行して起動します。`--headless` フラグは、画面を表示するデスクトップ環境がない Codespace でブラウザーを表示せずに実行するために必要です。

> [!NOTE]
> Tailspin Toys ではエンドツーエンド テストに Playwright を使うため、ブラウザーはすでにインストールされていることが多いです。Copilot がブラウザーの不足を報告した場合は、`npx playwright install chromium` を実行して再試行します。

## サーバーを起動して信頼する

VS Code は必要に応じて MCP サーバーを起動します。サーバーのツールが初めて必要になったときにサーバーを起動し、信頼するか確認します。

1. `.vscode/mcp.json` の `playwright` エントリの上に **Start** 操作が表示されます。選択してサーバーを起動し、設定が正しいことを確認します。
2. VS Code からサーバーを信頼するよう求められたら、設定を確認し、信頼して起動できるようにします。

手動で起動する必要はありません。省略した場合は、次の手順で Copilot がツールを必要としたときに VS Code が起動を促します。

## 絞り込み機能をテストする

[Playwright MCP サーバー][playwright-mcp-server]によって、Copilot は実際のブラウザーを操作できます。エージェントがページを開き、移動し、フィルターを適用して結果を読み取り、観察内容を要約できます。会話を離れずに機能を確認する方法です。

Playwright MCP サーバーはスクリーンショットではなく、ページの[アクセシビリティ ツリー][playwright-mcp-server]を使って動作します。エージェントはボタン、リンク、リスト項目など、ラベル付きの構造化された要素を使って推論します。これは支援技術と同じ方法なので、簡単な機能確認でアクセシビリティもある程度確認できます。

サーバーを接続してアプリを起動したら、次のプロンプトを Copilot に送ります。

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot は Playwright MCP サーバーでブラウザーを起動し、手順に沿って確認した内容を報告します。issue の受け入れ条件に照らして結果を確認してください。問題があれば追加で質問するか、PR を開く前にコードの修正を依頼します。

> [!NOTE]
> テストするにはアプリが `http://localhost:4321` で実行されている必要があります。開発サーバーを停止した場合は、プロンプトを送る前に再起動します。Playwright MCP サーバーの初回利用時にブラウザーをダウンロードすることがあります。不足が報告された場合は `npx playwright install chromium` を実行して再試行します。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## ブランチを公開してプル リクエストを作成する

機能が正しく動作することを確認したので、チームにレビューしてもらうためにプル リクエスト (PR) を作成します。最初に `filtering-vscode` ブランチを公開します。

1. Codespace で **Source Control** パネルに移動し、Copilot が行った変更をレビューします。
2. **+** アイコンを選択して変更をステージします。
3. **Sparkle** ボタンを使ってコミット メッセージを作成します。

   ![変更が表示された Source Control パネル](../../../_images/ex3-source-control-changes.png)

4. **Publish** を選択してブランチをリポジトリにプッシュします。

## プル リクエストを作成する

github.com や GitHub コマンド ライン インターフェイス (CLI) など、複数の方法でプル リクエストを作成できます。GitHub Copilot を利用しているため、Copilot に作成を依頼します。関連する issue を見つけ、PR と関連付けられます。

1. Copilot Chat パネルに移動し、**New Chat** を選択して新しいセッションを開始します。
2. GitHub ツールを使用できるように、エージェント ドロップダウンで **Agent** が選択されていることを確認します。
3. Copilot に PR の作成を依頼します。

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. 必要に応じて **Continue** を選択し、情報の取得や操作を許可します。GitHub ツールを初めて使うとき、GitHub への認証を求められることがあります。表示される手順に従います。
5. Copilot が issue を検索し、適切なものを見つけて PR を作成する様子を確認します。
6. Copilot が生成したリンクを選択して PR を確認しますが、**まだマージしないでください**。

## まとめと次のステップ

この演習では、次の操作を行いました。

- Model Context Protocol (MCP) と MCP サーバーが Copilot にツールを追加する仕組みを学びました。
- Playwright MCP サーバーをワークスペースに追加しました。
- リリース前に MCP サーバーを使ってブラウザーで絞り込み機能を手動テストしました。
- ブランチを公開し、絞り込み作業のプル リクエストを作成しました。

MCP サーバーを使って機能をテストしましたが、Copilot を拡張する方法は MCP だけではありません。次は[カスタム エージェントを作成します][next-lesson]。アクセシビリティ レビューのような限定的なタスクに活用できます。

## リソース

- [MCP とは何か、なぜ話題になっているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP レジストリ][mcp-registry]
- [VS Code の MCP サーバー][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
