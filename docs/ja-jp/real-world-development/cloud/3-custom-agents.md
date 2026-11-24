---
title: "演習 3 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]を使うと、開発ワークフロー内の特定のタスクや分野に合わせた AI アシスタントを作成できます。リポジトリの `.github/agents` にある Markdown ファイルでエージェントを定義し、対象の作業に役立つ指示、ベスト プラクティス、コーディング パターン、専門知識を伝えます。チームの知識を再利用できるエージェントとして共有できます。例としては、[WCAG][wcag] 準拠を確認するアクセシビリティ エージェント、安全なコーディングに従うセキュリティ エージェント、一貫したテスト パターンを守るテスト エージェントなどがあります。

カスタム エージェントは、プロジェクト内の `.github/agents` またはグローバルな `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには、少なくとも `name` と `description` を含む YAML フロントマターと、エージェントの動作、専門知識、指示を記述する Markdown プロンプトが必要です。

### カスタム エージェントとエージェント スキルの違い

カスタム エージェントと[エージェント スキル][agent-skills-concept]には重なる部分があります。どちらも主に Markdown ファイルで定義し、操作の実行方法を AI に伝えます。簡潔に区別すると、**カスタム エージェントは作業者、スキルはツール**です。

カスタム エージェントには独自のコンテキスト ウィンドウがあり、作業の一部としてスキルやほかのエージェントを組み合わせられます。このラボのアクセシビリティ エージェントは、サイトをアクセシビリティ ガイドラインに照らしてレビューし、更新します。その一環として、プル リクエスト ワークフローのスキルやテスト実行・管理のスキルを呼び出すこともできます。

> [!NOTE]
> カスタム エージェントの作成に唯一の正解はありません。AI のほかの機能と同様に、環境やシナリオに合わせて試し、反復してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

この演習では、次の操作を行います。

- カスタム エージェントの定義方法を確認します。
- カスタム エージェントにタスクを割り当てます。

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべての人がクラウドファンディング プラットフォームを使えるように取り組んでいます。現在のダーク テーマでは背景色と文字色のコントラストが不十分で、読みづらいと感じるユーザーがいるというフィードバックがありました。デザイン チームは、切り替え可能なハイ コントラスト モードを実装したいと考えています。

アクセシビリティは重要なため、カスタム エージェントを使って機能をすばやく生成します。

## アクセシビリティ カスタム エージェントを確認する

アクセシビリティ用のカスタム エージェントがすでに用意されています。内容を確認して、Copilot を導く方法を把握しましょう。

Codespace に戻り、アクセシビリティ エージェントのファイルを確認します。

1. `.github/agents/accessibility.md` を開きます。
2. `name` と `description` フィールドが含まれる YAML フロントマターを確認します。

> [!CAUTION]
> カスタム エージェントには `name` と `description` を含むフロントマターが必要です。

3. 続くセクションを読み、次の内容を確認します。
   - アクセシブルな Web サイトのコード生成に関する主要な責任。
   - アクセシビリティのベスト プラクティス。
   - HTML、CSS、JavaScript のコード例。
   - よくある落とし穴や間違い。

## issue を作成して割り当てる

Mission control は、環境内のエージェントを操作するための中心的な場所です。Copilot cloud agent にタスクを割り当て、進捗を監視し、作業中に追加のガイダンスを伝えられます。ハイ コントラスト モードを作成するタスクを Copilot に割り当てます。

1. リポジトリに移動します。
2. Issues タブを選択します。
3. **New issue** を選択して issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Add high contrast mode to website` と入力します。
6. **Description** に次を入力します。

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して割り当てダイアログを開きます。
9. カスタム エージェントの一覧から **Accessibility agent** を選択します。

   ![カスタム エージェントとアクセシビリティ エージェントが強調表示された cloud agent の割り当て画面](../../../_images/ex5-select-custom-agent.png)

10. **Assign** を選択します。
11. Copilot がバックグラウンドで作業を始めます。

## まとめと次のステップ

特定のタスクや分野に合わせた専門 AI アシスタントである、GitHub Copilot の[カスタム エージェント][custom-agents]を学びました。カスタム エージェントを使うと、チームの専門知識や標準を再利用し、Copilot を効果的に導けます。

このレッスンでは、次の操作を行いました。

- カスタム エージェントの定義方法を確認しました。
- エージェントにタスクを割り当てました。

Copilot がハイ コントラスト モードを実装している間に、[Mission control からエージェント セッションを監視して案内します][next-lesson]。

## リソース

- [カスタム エージェントについて][custom-agents]
- [組織でカスタム エージェントを使う準備][org-custom-agents]
- [エンタープライズでカスタム エージェントを使う準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
