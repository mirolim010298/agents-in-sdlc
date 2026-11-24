---
title: "演習 4 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]を使うと、開発ワークフローの特定のタスクや分野に合わせた AI アシスタントを作成できます。リポジトリの `.github/agents` にある Markdown ファイルでエージェントを定義し、対象の作業に役立つ指示、ベスト プラクティス、コーディング パターン、専門知識を伝えます。チームの知識を再利用できるエージェントとして共有できます。例としては、[WCAG][wcag] 準拠を確認するアクセシビリティ エージェント、安全なコーディングに従うセキュリティ エージェント、一貫したテスト パターンを守るテスト エージェントなどがあります。

カスタム エージェントは、プロジェクト内の `.github/agents` またはグローバルな `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには、少なくとも `name` と `description` を含む YAML フロントマターと、エージェントの動作、専門知識、指示を記述する Markdown プロンプトが必要です。

### カスタム エージェントとエージェント スキルの違い

カスタム エージェントと[エージェント スキル][agent-skills-concept]には重なる部分があります。どちらも主に Markdown ファイルで定義し、操作の実行方法を AI に伝えます。簡潔に区別すると、**カスタム エージェントは作業者、スキルはツール**です。

カスタム エージェントには独自のコンテキスト ウィンドウがあり、作業の一部としてスキルやほかのエージェントを組み合わせられます。このラボのアクセシビリティ エージェントは、サイトをアクセシビリティ ガイドラインに照らしてレビューし、更新します。その一環として、プル リクエスト ワークフローのスキルやテスト実行・管理のスキルを呼び出すこともできます。

> [!NOTE]
> カスタム エージェントの作成に唯一の正解はありません。AI のほかの機能と同様に、環境やシナリオに合わせて試し、反復してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべての人がクラウドファンディング プラットフォームを使えるように取り組んでいます。現在のダーク テーマでは背景色と文字色のコントラストが不十分で、読みづらいと感じるユーザーがいるというフィードバックがありました。デザイン チームは、切り替え可能なハイ コントラスト モードを実装したいと考えています。

アクセシビリティは重要なため、カスタム エージェントを使って機能をすばやく生成します。

この演習では、次の操作を行います。

- 既存のアクセシビリティ カスタム エージェントを確認します。
- Copilot Chat でアクセシビリティ エージェントを使い、ハイ コントラスト モードを実装します。

## アクセシビリティ カスタム エージェントを確認する

アクセシビリティ用のカスタム エージェントがすでに用意されています。内容を確認して、Copilot を導く方法を把握しましょう。

Codespace に戻り、ターミナルを開いて `main` からアクセシビリティ作業用のブランチを作成します。演習 3 の絞り込み PR とは分けて作業します。

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. `.github/agents/accessibility.md` を開きます。
2. `name` と `description` フィールドが含まれる YAML フロントマターを確認します。

> [!CAUTION]
> カスタム エージェントには `name` と `description` を含むフロントマターが必要です。

3. 続くセクションを読み、次の内容を確認します。
   - アクセシブルな Web サイトのコード生成に関する主要な責任。
   - アクセシビリティのベスト プラクティス。
   - HTML、CSS、JavaScript のコード例。
   - よくある落とし穴や間違い。

## Copilot Chat でカスタム エージェントを使う

VS Code では、`.github/agents` に定義したカスタム エージェントが、Copilot Chat ビュー下部のエージェント ドロップダウンに表示されます。選択すると、そのエージェントの指示とツールに基づいて Chat セッションが進みます。

> [!TIP]
> **Copilot Chat を開く**
>
> 次の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。モードとモデルの選択は演習ごとに異なり、必要な場合は手順で説明します。

1. Chat ビューのエージェント ドロップダウンから、まだ選ばれていない場合は **Agent** を選択します。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

2. Chat ビューの下部にあるエージェント ドロップダウンを選択します。アクティブなエージェントが表示されます。既定では **default** です。
3. 利用可能なエージェントの一覧から **Accessibility agent** を選択します。
4. アクセシビリティ エージェントに次のプロンプトを送ります。

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot Chat はコードベースを調査し、変更を提案して、プロジェクト ファイルを編集します。編集はファイル パスと差分とともに Chat に表示されます。
6. エージェントが変更した作業セットに合わせて **Files changed** の表示が更新されます。

> [!NOTE]
> この作業には数分かかることがあります。Copilot は Astro コンポーネント、CSS、関連テストなどのファイルを変更します。

次の演習では、進行中の作業をレビューし、追加の指示を伝えます。

## まとめと次のステップ

GitHub Copilot の[カスタム エージェント][custom-agents]を学びました。特定のタスクや分野に特化した AI アシスタントを使い、チームの専門知識と標準を再利用できます。

このレッスンでは、次の操作を行いました。

- カスタム エージェントの定義方法を確認しました。
- Copilot Chat のエージェント モードでカスタム エージェントを使いました。

次は[エージェントの作業を監視して案内し][next-lesson]、変更を確認しながら、同じセッションにライト モードの切り替えを追加します。

## リソース

- [カスタム エージェントについて][custom-agents]
- [IDE でカスタム エージェントを作成する][creating-custom-agents-ide]
- [VS Code のカスタム エージェント][custom-agents-vscode]
- [カスタム エージェントの設定][custom-agents-config]
- [awesome-copilot のカスタム エージェント][awesome-copilot-agents]

---

| [← 前のレッスン: Playwright MCP サーバーで機能をテストする][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
