---
title: "レッスン 0 - 前提条件"
description: "Tailspin Toys の自分用コピーを作成し、Copilot CLI ワークショップ用に GitHub Codespace を準備します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI のレッスンを始める前に、必要なものを準備します。Tailspin Toys リポジトリの自分用コピーを作成し、[Codespace][codespaces] を起動します。次のレッスンでは、統合ターミナルを使って Copilot CLI をインストールし、実行します。

このレッスンでは、次の操作を行います。

- テンプレートから Tailspin Toys プロジェクトの自分用コピーを作成します。
- Codespace を作成し、プロジェクトの準備ができていることを確認します。

## ラボ リポジトリをセットアップする

Tailspin Toys プロジェクトの自分用コピーを使います。[テンプレート リポジトリ][tailspin-template]から今すぐ作成してください。新しいリポジトリには、ラボで必要なファイルがすべて含まれます。

1. 新しいブラウザー ウィンドウで [Tailspin Toys テンプレート][tailspin-template]に移動します。
2. **Use this template** を選択し、次に **Create a new repository** を選択してリポジトリのコピーを作成します。
3. GitHub または Microsoft 主催のイベントでワークショップに参加する場合は、メンターの指示に従います。それ以外の場合は、GitHub Copilot を利用できる組織にリポジトリを作成します。
4. 作成したリポジトリのパス (`organization-or-user-name/repository-name`) をメモしておきます。ワークショップ中に参照します。

> [!NOTE]
> テンプレートからリポジトリを作成すると、GitHub issue のバックログも自動で作成されます。ワークショップ中はこれらの issue を使うため、自分で登録する必要はありません。

ワークショップ テンプレートの新しいコピーを使ってください。必要な指示ファイル、アプリケーション コード、テスト、`quality-checks` スキル、バックログが含まれています。古いコピーを使用している場合は、必要なファイルが含まれていることを進行役に確認してください。

## Codespace を作成する

次は Codespace を使ってワークショップを進めます。

[GitHub Codespaces][codespaces] は、ブラウザーで直接コードを書き、実行し、デバッグできるクラウド開発環境です。複数のプログラミング言語、拡張機能、ツールを利用できる、フル機能のエディターを提供します。

1. 作成したリポジトリを開きます。
2. **Code** を選択します。
3. **Codespaces** タブを選び、**Create codespace on main** を選択します。
4. Codespace のセットアップが完了するまで待ちます。テンプレートがプロジェクトの依存関係、Playwright Chromium、ローカル データベースを準備します。
5. **Do you trust the authors of the files in this folder?** と表示されたら、**Trust Folder & Continue** を選択します。
6. リポジトリのルートでターミナルを開き、アプリケーションを起動します。

   ```bash
   npm run dev
   ```

7. Codespaces でポート `4321` が利用可能になったら **Open in Browser** を選択し、Tailspin Toys が表示されることを確認します。
8. ターミナルに戻り、<kbd>Ctrl</kbd>+<kbd>C</kbd> で開発サーバーを停止します。

## まとめと次のステップ

セットアップが完了しました。このレッスンでは、次の操作を行いました。

- テンプレートから Tailspin Toys プロジェクトの自分用コピーを作成しました。
- Codespace を作成し、プロジェクトの準備ができていることを確認しました。

次は Codespace に[GitHub Copilot CLI をインストール][next-lesson]し、GitHub アカウントで認証します。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces の使用を開始する][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-install-copilot-cli/
[codespaces]: https://github.com/features/codespaces
