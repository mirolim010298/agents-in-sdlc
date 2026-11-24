---
title: "演習 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。タスクを特定の方法で進める必要がある場合や、Copilot に背景情報を知らせる必要がある場合は、そのコンテキストを参照できるようにします。[指示ファイル][instruction-files]を使ってガイダンスを伝え、Copilot に実行内容だけでなく方法も理解させます。

この演習では、次の操作を行います。

- リポジトリのカスタム指示とパス別の指示ファイルを通じて、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に伝わる仕組みを確認します。
- `.github/copilot-instructions.md` にリポジトリ全体の標準を追加します。

> [!NOTE]
> VS Code や CLI のハーネスと異なり、この演習ではプロンプトの実行前後を比較しません。Copilot cloud agent は GitHub issue を非同期で処理するため、リアルタイムの比較が難しいためです。後続の演習で、cloud agent が作成したプル リクエストを確認する際に指示ファイルの影響を見ます。

## 指示ファイル

### シナリオ

Tailspin Toys では、次のような開発手法に関するガイドラインと要件があります。

- データ レイヤーには必ず単体テストを用意します。
- UI はダーク モードにし、現代的な見た目にします。
- TSDoc のドキュメント コメントをコードに追加します。
- 各ファイルの先頭に、ファイルの内容を説明するコメント ブロックを追加します。

指示ファイルを使い、Copilot がこれらの慣例に沿ってタスクを実行できるようにします。

### カスタム指示

カスタム指示を使うと、コーディング スタイルや要件を Copilot に伝え、適切なコードの提案を得られます。推奨するコーディング規約、ライブラリ、コメントの書き方などを指定できます。リポジトリ全体に適用する指示も、特定のファイルだけに適用する指示も作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリへの**すべての**要求に使われます。多くの Copilot Chat または CLI の要求に関係するプロジェクト全体の情報を記載します。技術スタック、開発中の内容、ベスト プラクティス、全般的なガイダンスなどが含まれます。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイルの種類に指示を適用します。TypeScript や Astro などの言語、UI コンポーネントや単体テストの作成などのタスクを対象にできます。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリ レベルの指示と `applyTo` フロントマターを持つ `*.instructions.md` ファイルの両方を使ってコードを生成します。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの標準を使った指示ファイルにも対応しています。詳細は[カスタム指示のサポート][custom-instructions-support]をご覧ください。

### 指示ファイルを管理するためのベスト プラクティス

指示ファイルの作成を詳しく扱うことは、このワークショップの範囲外です。サンプル プロジェクトの例から、代表的な方法を確認できます。

- `copilot-instructions.md` には、構築中のもの、プロジェクト構成、全般的なコーディング標準など、プロジェクト レベルのガイダンスを記載します。
- `*.instructions.md` は、単体テスト、Astro コンポーネント、データ レイヤーなどのファイルの種類や、特定のタスクに関する指示に使います。
- 自然な言葉で、明確なガイダンスと、コードのよい例・避けるべき例を示します。

指示ファイルの作成方法は 1 つではありません。AI の使い方と同様、プロジェクトに合う方法は試しながら見つけます。

> [!TIP]
> GitHub Copilot を使うすべてのプロジェクトに、充実した指示ファイルを用意することをお勧めします。このプロジェクトには [UI 更新][ui-instructions]や [Astro][astro-instructions]など、さまざまなタスク向けの指示があります。
>
> Copilot に指示ファイルを生成させることもできます。VS Code では **Configure Chat → Generate Agent Instructions**、Copilot CLI では `/init` など、環境によって方法が異なります。各環境のレッスンで説明します。
>
> テンプレートや出発点を探す場合は、指示ファイル、カスタム エージェントなどを集めた [awesome-copilot][awesome-copilot] をご覧ください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

リポジトリに含まれる指示ファイルを読みます。中心となる `copilot-instructions.md` と、タスク別の `*.instructions.md` ファイルがあります。エディターまたは GitHub Web UI から開いてください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの説明と **Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** 内の **GitHub Actions Workflows** の指示にも注目します。これらは Copilot とのすべてのやりとりに適用されます。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データ レイヤー、テストなどの指示を確認します。
4. `.github/instructions/unit-tests.instructions.md` を開きます。`applyTo` フィールドがリポジトリのルートからの glob を指定します。ここでは、`**/*.test.ts` に一致する TypeScript のテスト ファイルが対象です。
5. このプロジェクトで単体テストを作成する際の指示を確認します。
6. `.github/instructions/drizzle.instructions.md` を開き、末尾にある他の指示ファイル (例: `unit-tests.instructions.md`) や既存ファイルへのリンクを確認します。これにより大きな指示を再利用できる小さなファイルに分け、Copilot に例を示せます。ここにあるパスはリポジトリ ルートではなく、指示ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトの標準が記載されていますが、コード内のドキュメントはまだ必須ではありません。次の手順で TSDoc コメントとファイル ヘッダーの規則を追加します。

## 新しいリポジトリ標準を追加する

ここで行う編集は、コード内のドキュメントとして TSDoc コメントとファイル レベルのコメント ヘッダーを必須にすることです。後続の演習で issue を割り当てるとき、cloud agent がこの標準を使います。

編集の前に、作業用のブランチを用意します。cloud agent は issue の対象ブランチから指示を読みますが、変更をコミットするためにブランチを作成します。

1. Codespace のターミナルで新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` に、リポジトリ全体へ適用する指示を追加します。

1. `.github/copilot-instructions.md` を開き直します。
2. 27 行目付近にある **Code formatting requirements** セクションを見つけます。コーディング標準が記載されていますが、生成されたヘルパーにドキュメント コメントがなかったのは、コード内ドキュメントの規則がなかったためです。
3. 既存の標準の直後に、次の Markdown を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 指示ファイルはリポジトリ レベル (`.github/copilot-instructions.md`) で全体的に適用することも、特定の言語、ファイルの種類、タスク向けに `*.instructions.md` として作成することもできます。ここで追加したドキュメント コメントの規則など、プロジェクト全体の標準はリポジトリ レベルのファイルに記載します。

## 指示の更新をコミット、プッシュ、マージする

cloud agent は issue の対象ブランチにある指示ファイルを読み込みます。次の演習で issue を割り当てるとき、Copilot は `main` からブランチを作成するため、更新した指示を `main` にマージする必要があります。

1. ステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` へのプル リクエストを開いてマージします。次の演習で issue を割り当てるとき、cloud agent はこの指示を読み込みます。

> [!TIP]
> このワークショップで `main` に直接作業したい場合は、ブランチを作成せずに `main` へコミットしてもかまいません。実際のプロジェクトでの手順を示すため、ここではブランチを使います。

## まとめと次のステップ

Copilot がこのプロジェクトの指示ファイルからコンテキストを得る仕組みを確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。残りのハーネスで cloud agent が作成するプル リクエストをレビューするときに、この標準が適用されていることを確認します。

次は[最初の issue を Copilot cloud agent に割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot 向けのカスタム指示を改善する 5 つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
