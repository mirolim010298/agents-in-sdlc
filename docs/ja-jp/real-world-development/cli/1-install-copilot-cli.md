---
title: "レッスン 1 - GitHub Copilot CLI をインストールする"
description: "Codespace に Copilot CLI をインストールして認証し、基本を確認して、登録済みの絞り込み issue を見つけます。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] は、ターミナルで動作する強力なエージェント型コーディング アシスタントです。コードベースの調査、コードの生成、コマンドの実行、外部ツールとの連携をコマンド ラインから行えます。タスクを任せたり、変更を依頼したりしながら、集中して作業できます。最初のステップとしてツールをインストールします。すでに使い慣れているツールを使って簡単に実行できます。

このレッスンでは、次の操作を行います。

- npm を使って GitHub Copilot CLI をインストールします。
- GitHub アカウントで認証します。
- ワークショップのリポジトリを信頼し、簡単な会話を試します。
- 組み込みの GitHub MCP サーバーで絞り込み issue を見つけます。

## シナリオ

チームでは、増え続けるバックログに対応するため、AI エージェントを使い始めています。Copilot CLI は、多くの開発者が日常的に作業するターミナルでその機能を使えるようにします。このレッスンではインストールと認証を済ませ、ワークショップの残りで利用できる状態にします。

## Copilot CLI をインストールする

Copilot CLI は [npm][install-cli]、WinGet、Homebrew からインストールできます。GitHub Codespaces には Node.js が事前にインストールされているため、npm を使います。

1. Codespace に戻り、ターミナルを開きます。
2. Node.js がインストールされ、必要なバージョンを満たしていることを確認します。

   ```bash
   node --version
   ```

   バージョン 24 以上が表示されます。

3. Copilot CLI をグローバルにインストールします。

   ```bash
   npm install -g @github/copilot
   ```

4. インストールを確認します。

   ```bash
   copilot --version
   ```

   バージョン番号が表示されます。

## GitHub で認証する

初回起動時に、Copilot CLI は GitHub アカウントでの認証を求めます。

1. Copilot CLI を起動します。

   ```bash
   copilot
   ```

2. 認証を求められた場合は、device code の手順に従って認証し、Copilot CLI を許可します。
3. Copilot CLI に次のプロンプトが表示されます。

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. パスが Tailspin Toys リポジトリであることを確認し、**Yes, and remember this folder for future sessions** を選択して信頼します。

> [!NOTE]
> Codespace では GitHub セッションを通じて認証済みの場合があります。Copilot CLI が認証を求めずに起動した場合は、そのまま進めて問題ありません。

## 基本を確認する

通常のシェル プロンプトでは、コマンドは Codespace で直接実行されます。Copilot CLI の起動後は、自然言語をエージェントに送り、スラッシュ コマンドで会話を操作します。

1. `/model` を入力し、矢印キーで **Auto** を選択して <kbd>Enter</kbd> を押し、もう一度 <kbd>Enter</kbd> を押して確定します。
2. `/help` を入力してインストール済みバージョンのコマンドを確認し、<kbd>Esc</kbd> を押してヘルプ画面を閉じます。
3. 簡単な質問をして動作を確認します。

   ```plaintext
   What are the key files in this project?
   ```

4. 応答を読み、Copilot が回答前にリポジトリを調べることを確認します。
5. `/mcp list` を実行し、組み込みの GitHub MCP サーバーが利用可能であることを確認します。
6. Copilot に絞り込み issue を見つけるよう依頼します。

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. URL を開き、issue を読みます。最初の変更に取り組んだ後、この issue を使います。

> [!TIP]
> 通常の Copilot CLI セッションは、ターミナルで現在チェックアウトされているブランチを使い、自動的には worktree を作成しません。各変更の前に機能ブランチを作成します。

## ワークショップ用のショートカットを使う

Copilot CLI は、許可されている範囲外のツールを使う前に通常確認を求めます。このワークショップでは `--yolo` を使って再起動します。Codespace 内の承認プロンプトを省略し、演習に集中できます。

> [!CAUTION]
> `--yolo` は `--allow-all-tools`、`--allow-all-paths`、`--allow-all-urls` を含むすべての自動権限を有効にします。Codespace や VM などの隔離された環境でのみ使い、日常の開発で既定のエイリアスにしないでください。詳細は[ツールの使用を許可または禁止する][allow-all-warning]を参照してください。

後のレッスンで issue やプル リクエストを操作するため、`--enable-all-github-mcp-tools` で読み書き可能な GitHub MCP ツールを有効にします。Codespace からローカル コンピューターへのアクセスは制限されていますが、認証済みの GitHub リソースは実際のものです。公開やマージの前に変更を確認してください。

1. `/exit` で Copilot CLI を終了します。
2. リポジトリのルートから再起動します。

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. プロジェクトについて簡単な質問を送り、会話が動作することを確認してから `/exit` で終了します。

Copilot は会話を自動的に保存します。後で指示を変更したりエージェントを追加したりしたら、`copilot --resume` を使って同じ機能の会話とブランチに戻ります。

## まとめと次のステップ

おめでとうございます。このレッスンでは、次の操作を行いました。

- npm を使って GitHub Copilot CLI をインストールしました。
- GitHub アカウントで認証しました。
- ワークショップのリポジトリを信頼し、簡単な会話を試しました。
- 組み込みの GitHub MCP サーバーで絞り込み issue を見つけました。

次は[最初の小さな変更を始め][next-lesson]、Copilot CLI でゲーム カードに星評価を表示します。

## リソース

- [GitHub Copilot CLI をインストールする][install-cli]
- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
