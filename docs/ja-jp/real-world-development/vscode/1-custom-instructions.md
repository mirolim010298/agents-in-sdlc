---
title: "演習 1 - カスタム指示 (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: エージェント モード →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。タスクを特定の方法で進める必要がある場合や、Copilot に背景情報を伝える必要がある場合は、そのコンテキストを参照できるようにします。コード生成の指針となる[指示ファイル][instruction-files]を使って、Copilot にその方法を伝えます。

この演習では、次の操作を行います。

- リポジトリのカスタム指示とパス別の指示ファイルを通じて、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に伝わる仕組みを確認します。
- 現在の指示を使って、絞り込み用の最初のデータ スライス (販売元ヘルパー) を作成します。
- `.github/copilot-instructions.md` に新しいリポジトリ全体の標準を追加します。
- 同じプロンプトを再実行し、生成コードが新しい標準に従うことを確認します。
- 指示の更新と絞り込み用データ スライスを `main` にコミットし、次の演習で新しい指示を使えるようにします。

> [!CAUTION]
> 生成コードが設定した標準の一部に従わないことがあります。Copilot は確率的に動作します。この演習の目的は、更新後に動作がどのように変化するかを見ることであり、生成結果を文字単位で一致させることではありません。

## 指示ファイル

### シナリオ

Tailspin Toys には、次のような開発手法に関するガイドラインと要件があります。

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

指示ファイルの作成方法は 1 つではありません。AI のほかの機能と同様、プロジェクトに合う方法は試しながら見つけます。

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
2. **Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** 内の **GitHub Actions Workflows** の指示にも注目します。これらは Copilot とのすべてのやりとりに適用されます。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データ レイヤー、テストなどの指示を確認します。
4. `.github/instructions/unit-tests.instructions.md` を開きます。`applyTo` フィールドがリポジトリのルートからの glob を指定します。ここでは、`**/*.test.ts` に一致する TypeScript のテスト ファイルが対象です。
5. このプロジェクトで単体テストを作成する際の指示を確認します。
6. `.github/instructions/drizzle.instructions.md` を開き、末尾にある他の指示ファイル (例: `unit-tests.instructions.md`) や既存ファイルへのリンクを確認します。これにより大きな指示を小さく再利用可能なファイルに分け、Copilot に例を示せます。ここにあるパスは指示ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトの標準が記載されていますが、コード内のドキュメントはまだ必須ではありません。次の手順で TSDoc コメントとファイル ヘッダーの規則を追加します。

## 変更用ブランチを作成する

変更用のブランチを作成して、ベスト プラクティスに沿って進めます。

1. 前の演習で使った Codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して新しいターミナルを開きます。
3. 新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## 指示を更新する前に Copilot Chat を使う

> [!TIP]
> **Copilot Chat を開く**
>
> 次の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。モードとモデルの選択は演習ごとに異なり、必要な場合は手順で説明します。

カスタム指示の影響を確認するため、まず現在の指示ファイルを使ってプロンプトを送ります。その後ファイルを更新し、同じプロンプトを再送信して違いを見ます。

1. 前の演習のエディター タブを閉じ、Copilot が意図したコンテキストだけを使うようにします。
2. Copilot にヘルパーの場所を知らせるため、`src/lib/publishers.ts` を開きます。
3. Chat ビューのエージェント ドロップダウンから **Agent** を選び、ファイルを変更できるようにします。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot はプロジェクトを調べ、ヘルパーとテストを含むファイルを更新します。
6. 提案されたヘルパーが、型付けされた関数として `db` クライアントを最初の引数に取り、型付きの販売元配列を返すことを確認します。これは `src/lib/*.ts` に適用される `.github/instructions/drizzle.instructions.md` の慣例です。
7. 生成されたコードに TSDoc コメントとファイル レベルのコメント ヘッダーが**ない**ことを確認します。

> [!CAUTION]
> Copilot は確率的に動作するため、指示がなくても TSDoc コメントが追加される場合があります。その場合も問題ありません。指示を更新した後の一貫性向上が重要です。

## 新しいリポジトリ標準を追加する

`.github/copilot-instructions.md` は、Copilot にプロジェクト全体の情報を与えるためのファイルです。コード提案を改善するため、コーディング標準を追加します。

1. `.github/copilot-instructions.md` を開き直します。
2. 27 行目付近にある **Code formatting requirements** を見つけます。既存の標準は記載されていますが、コード内ドキュメントの規則がありません。
3. 既存の標準の直後に、次の Markdown を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> リポジトリ全体に適用する規則は `.github/copilot-instructions.md` に、特定の言語、ファイルの種類、タスク向けの指示は `*.instructions.md` に記載できます。ここで追加するドキュメント コメントのようなプロジェクト全体の標準には、リポジトリ レベルのファイルを使います。

## プロンプトを再実行して変化を確認する

1. Copilot Chat に戻り、**New Chat** を選択してコンテキストをクリアします。
2. `src/lib/publishers.ts` を開き、Copilot に対象ファイルを示します。
3. 前と**同じプロンプト**を送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 提案されたファイルの先頭に、次のようなコメント ブロックが追加されることを確認します。

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 提案された関数に次のような TSDoc コメントが含まれることを確認します。

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

新しいプロジェクト標準を Copilot に伝え、次の演習で使うコードに適用しました。

## 指示とブランチをコミットする

指示ファイルもほかのリポジトリ資産と同じようにソース管理します。変更をコミットしてブランチをプッシュします。

1. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
2. 指示の更新とヘルパーの変更を確認します。

   ```bash
   git status
   ```

3. 指示ファイルと Copilot がヘルパーの基礎作成で変更したすべてのファイルをステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # git status に追加の関連ファイル (例: テスト) が表示される場合は、それらも追加します。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. リポジトリにブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions
   ```

## プル リクエストを作成してマージする

ブランチをプッシュしたら、バックログのドキュメント標準に関する issue と関連付けてプル リクエストを作成します。GitHub ツールはすでにプロジェクトに接続されているので、Copilot に依頼できます。

> [!NOTE]
> Copilot に GitHub 操作を依頼するのは初めてです。プロジェクト テンプレートでは GitHub ツールがすでに設定されていますが、初回利用時に VS Code から GitHub へのサインインを求められることがあります。後の演習では、この接続で使われる Model Context Protocol を学びます。

1. Codespace で Copilot Chat を開きます。
2. <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) を押して Copilot Chat ビューを開き、エージェント ピッカーで **Agent** を選択します。
3. 現在のブランチから PR を作成し、指示の更新と販売元ヘルパーの追加を説明するよう Copilot に依頼します。

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot が issue を探して PR を作成します。
5. GitHub 操作の **Allow** を求められたら、コマンドを確認して許可します。
6. PR が作成されたら、次のプロンプトでマージしてローカル ブランチを `main` に戻すよう依頼します。

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. GitHub 操作やシェル コマンドを許可するよう求められた場合は、内容を確認して許可します。

GitHub Copilot の支援でプル リクエストを作成し、マージできました。

## まとめと次のステップ

Copilot が指示ファイルからコンテキストを取得する仕組みを確認し、VS Code の Copilot Chat を使って次の操作を行いました。

- 既存の指示を使ってコード生成プロンプトを送り、提案を確認しました。
- `.github/copilot-instructions.md` に新しいリポジトリ全体の標準を追加しました。
- 同じプロンプトを再送信し、生成コードが新しい標準に従うことを確認しました。
- 次の演習が利用できるよう、指示の更新とヘルパーの基礎を `main` にコミットしました。

次は[エージェント モード][next-lesson]で指示を使い、コードベース全体に新機能を追加します。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot 向けのカスタム指示を改善する 5 つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人用カスタム指示][personal-instructions]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
