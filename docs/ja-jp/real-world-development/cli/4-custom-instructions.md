---
title: "レッスン 4 - カスタム指示で Copilot を導く"
description: "リポジトリの指示を確認し、ドキュメント標準を追加して、絞り込みのコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使うときは、コンテキストが重要です。特定の方法でタスクを進める必要があるなら、そのガイダンスを Copilot が参照できるようにします。[指示ファイル][instruction-files]では、求めるコードの内容だけでなく、その構成方法も伝えられます。絞り込み機能を実装したので、Copilot が参照した指示を確認し、ドキュメント標準を追加して、コードに適用します。

このレッスンでは、次の操作を行います。

- リポジトリの指示とパス別の指示ファイルがエージェントに適用される仕組みを確認します。
- コーディング標準を守るために指示ファイルを更新します。
- 指示ファイルがコードに与える影響を確認します。

## シナリオ

Tailspin Toys には、開発手法に関するガイドラインと要件があります。

- コメントには、コードの言い換えではなく、意図や自明でない決定を記載します。
- `db/` と `src/lib/` のエクスポート関数には、目的、パラメーター、戻り値を説明する TSDoc/JSDoc を記載します。該当する場合は、注入可能な `db` 引数も説明します。
- 再利用可能な Astro コンポーネントでは `Props` の契約を説明し、関連コードが変更されたらコメントも最新の状態にします。
- 既存のフォーマットと lint のガイダンスを維持します。

指示ファイルを使い、Copilot がこれらの慣例に沿ってタスクを実行できるようにします。

## 指示ファイル

カスタム指示を使うと、コーディング スタイルや要件を Copilot に伝え、適切なコードの提案を得られます。推奨するコーディング規約、ライブラリ、コメントの書き方などを指定できます。リポジトリ全体に適用する指示も、特定の種類のファイルだけに適用する指示も作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリへの**すべての**要求に使われる単一の指示ファイルです。多くの要求に関係するプロジェクト全体の情報を記載します。
- `.github/instructions/*.instructions.md` は、言語、ファイルの種類、タスクごとのガイドラインを提供します。

> [!NOTE]
> ほかの形式の指示とそのサポート状況は、環境によって異なります。特定の形式に依存する前に、[カスタム指示のサポート リファレンス][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム指示ファイルを確認する

スターター プロジェクトには、あらかじめ複数の指示ファイルが含まれています。変更を加える前に、現在の内容を確認しましょう。

1. Codespace に戻ります。
2. Codespaces エディターで (ターミナルではなく) `.github/copilot-instructions.md` を開きます。
3. プロジェクトの簡単な説明とコーディング ガイダンスを確認します。この指示は、リポジトリでの Copilot とのすべてのやりとりに適用されます。
4. `.github/instructions` フォルダーを開き、ファイルを確認します。Astro、Drizzle データ レイヤー、テストなどの指示があります。
5. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドが、適用対象のファイルを決める glob を指定しています。
6. `.github/instructions/drizzle.instructions.md` を開き、ほかの指示ファイルや既存プロジェクト ファイルへのリンクを確認します。大きな指示を小さく再利用可能なファイルに分け、参照例を示せます。

## チームの方針に合わせて指示ファイルを更新する

既存の指示はよい出発点ですが、生成される TypeScript に TSDoc コメントを追加する標準が不足しています。会話を再開し、新しいガイダンスを適用します。

1. `.github/copilot-instructions.md` の **Code formatting guidance** セクション (35 行目付近) を見つけます。
2. 最後の箇条書きとして、次を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

ファイルは自動的に保存されます。

## 更新したガイダンスを使う

Copilot CLI は会話の開始時にリポジトリの指示を読み込みます。指示を保存したら、終了して絞り込みの会話を再開します。機能のコンテキストを保ったまま新しい指示を読み込めます。

1. 絞り込みの会話が開いている場合は `/exit` を入力します。Copilot CLI は会話を自動的に保存します。
2. リポジトリのルートから `game-filters-cli` ブランチで保存済みの会話を再開します。

   ```bash
   copilot --resume
   ```

   選択を求められた場合は絞り込みの会話を選び、`game-filters-cli` ブランチがチェックアウトされていることを確認します。
3. Copilot に更新したガイダンスを適用するよう依頼します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を実行し、変更された TypeScript ファイルを確認します。追加された TSDoc コメントがコードの内容を正確に説明していることを確認します。

## まとめと次のステップ

Copilot CLI が指示ファイルからコンテキストを取得する仕組みを確認し、新しい標準を機能に適用しました。具体的には、次の操作を行いました。

- リポジトリの指示とパス別の指示ファイルがエージェントに適用される仕組みを確認しました。
- 指示ファイルを更新して、コーディング標準を守れるようにしました。
- 指示ファイルがコードに与える影響を確認しました。

次は[再利用可能な quality-checks スキルをカスタマイズして実行し][next-lesson]、lint とテストが一貫して実行されるようにします。

## リソース

- [Copilot CLI のカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [効果的なカスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
