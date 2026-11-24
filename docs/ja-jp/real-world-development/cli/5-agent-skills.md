---
title: "レッスン 5 - quality-checks スキルをカスタマイズして使う"
description: "既存の quality-checks スキルを確認し、レポート形式をカスタマイズして、絞り込み機能の検証に使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

コードを書くこと以外にも、必要な作業はあります。これまでは手動でコードを検証し、指示ファイルでコーディング標準を守ってきました。テストや lint、継続的インテグレーション (CI) のほかの作業はどうでしょうか。

こうしたタスクには、**エージェント スキル**が適しています。スキルによって、こうした操作を正しく実行する方法を Copilot に伝えられます。

このレッスンでは、次の操作を行います。

- 既存の `quality-checks` スキルを確認します。
- 結果の表示形式をカスタマイズします。
- スキルを再読み込みして実行します。

## シナリオ

Tailspin Toys では、単体テスト、lint、型チェックに `quality-checks` スキルを使います。チームは、結果を読みやすくするため、レポートを改善したいと考えています。

## 指示、スクリプト、リソース

エージェント スキルには、再利用可能なタスクの指示、実行可能なスクリプト、補助リソースをまとめられます。基本的には、スキル名のフォルダーと、その中の `SKILL.md` で構成されます。Markdown には、スキルの内容と呼び出すタイミングを定義する `name` と `description` のフロントマターが含まれます。また、スクリプトや補助リソースのサブフォルダーを含めることもできます。

> [!NOTE]
> スキルに追加のフォルダーやファイルは必須ではありません。Tailspin Toys の `quality-checks` スキルは、プロジェクト既存のコマンドを使うため、`SKILL.md` だけで構成されています。

スキルはプロジェクトの `.github/skills` に置いてチームで共有するか、ユーザーの `~/.copilot/skills` に置けます。

## スキルを確認する

Tailspin Toys のチームが単体テスト、lint、型チェック用に作成した `quality-checks` スキルを確認します。

1. Codespace に戻り、Codespaces エディターで `.github/skills/quality-checks/SKILL.md` を開きます。
2. 冒頭の `name` と `description` を読みます。説明により Copilot はスキルを呼び出すタイミングを判断できます。
3. 指示を読み、Copilot がテストと lint を実行する方法を確認します。
4. **Results output formatting** セクションがまだないことを確認します。

## 変更前にスキルを実行する

Copilot CLI からスキルを直接呼び出すことも、自然言語で依頼することもできます。3 種類のチェックを実行します。

1. Interactive モードで絞り込みの会話に戻ります。
2. 次のプロンプトを入力します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後に表示されるレポートを確認します。

## レポートをカスタマイズする

実行したコマンド、成功したかどうか、ツールが報告した内容がわかるレポートに改善します。

1. `.github/skills/quality-checks/SKILL.md` に戻ります。
2. 次のセクションをファイルの末尾に追加します。

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. ファイルは自動的に保存されます。

## 更新したスキルを実行する

Copilot CLI は会話を再起動せずに、編集されたスキルを再読み込みできます。

1. 次のコマンドを入力します。

   ```plaintext
   /skills reload
   ```

2. 先ほどと同じプロンプトを入力します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最初のレポートと比べて内容を確認します。

## まとめと次のステップ

既存のエージェント スキルをカスタマイズして使いました。このレッスンでは、次の操作を行いました。

- 単体テスト、lint、型チェック用の `quality-checks` スキルを確認しました。
- 結果の表示形式をカスタマイズしました。
- スキルを再読み込みして実行しました。

この変更は絞り込み機能の PR に含めます。次は[Playwright MCP サーバーを使って][next-lesson]、Copilot がサイトを直接操作できるようにします。

## スキルの例

次のコミュニティの例は参考資料であり、追加タスクではありません。

- [Agent Skills 仕様][skill-spec]
- [コントリビューション ワークフロー: `make-repo-contribution`][contribution-example]
- [要件ドキュメント: `prd`][prd-example]
- [図とバンドルされたエクスポート スクリプト: `drawio`][drawio-example]
- [ブラウザー テスト: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
