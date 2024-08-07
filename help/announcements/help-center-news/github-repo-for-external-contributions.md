---
title: Adobe Commerce サポートナレッジベースがコントリビューションの受け入れを開始
description: 6 月 15 日（PT）より、Adobe Commerce サポートナレッジベースチームが、[magento/knowledge-base] （https://github.com/magento/knowledge-base） GitHub リポジトリーを通じて、外部Adobe Commerce コミュニティから直接編集や新しい記事の投稿を受け付け始めます。
exl-id: b5198de0-d6b5-4107-8b74-a12606583596
feature: Support
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Adobe Commerce サポートナレッジベースがコントリビューションの受け入れを開始

6 月 15 日（PT）より、Adobe Commerce サポートナレッジベースチームは、[magento/knowledge-base](https://github.com/magento/knowledge-base) GitHub リポジトリーを通じて、外部のAdobe Commerce コミュニティから直接編集や新しい記事の投稿を受け付け始めます。

記事の 1 つに誤字があるか、トラブルシューティング手順が不完全です。
これで、自分で修正して投稿ポイントを獲得できます。

## Contribute

軽微な誤字修正から完全なトラブルシューティング記事まで、あらゆる種類の投稿を歓迎します。 このリポジトリに投稿すると、Adobe Commerce コードや開発者向けドキュメントに投稿するのと同様に、報酬ポイントを取得できます。 詳しくは、[ 貢献度報酬ポイント ](https://github.com/magento/knowledge-base/blob/main/docs/contribution-points.md) を参照してください。

### 一般的な貢献度フロー

1. このリポジトリをフォークします。
1. フォークされたリポジトリで編集を行います。
1. このリポジトリにプルリクエスト（PR）を送信します。
1. テストが実行されます。
   * AdobeCLA - AdobeのオープンSource投稿者使用許諾契約に署名していることを確認します。
   * Markdown リンティングテスト - markdown 構文が正しいことを確認します。
   * ファイル構造検証テスト - [ 必要なファイル構造 ](https://github.com/magento/knowledge-base/blob/main/.github/CONTRIBUTING.md#file_structure) に従ってコミットが行われていることを確認します。
1. PR 承認フロー：
   1. サポートナレッジベース（KB）ライターは、数日以内に PR を確認し、ラベルを追加します。
   1. KB ライターは変更を承認/拒否/要求できます。
   1. 承認されると、ナレッジライターは PR で提供された入力レベルに対応するラベルを追加し、社内の対象分野のエキスパート（SME）は PR をレビューします。
   1. SME は、変更を承認/拒否/リクエストできます。
1. すべての修正が完了し（要求がある場合）、ナレッジライターと SME の両方が PR を承認すると、ナレッジライターはコンテンツを内部リポジトリに読み込み、内部で結合します。
1. [magento/knowledge-base](https://github.com/magento/knowledge-base) リポジトリは、20 分で内部リポジトリと同期されます。
1. リポジトリが同期されると、PR がクローズされ、[ 投稿ポイント ](#contribution-points) が取得されます。

投稿フローについて詳しくは、[ 投稿者ガイド ](https://github.com/magento/knowledge-base/blob/main/.github/CONTRIBUTING.md) を参照してください。
テンプレート、スタイルガイドおよび書式設定のガイドラインについては、[ ドキュメント ](https://github.com/magento/knowledge-base/tree/main/docs) を参照してください。

### Github でサポート技術情報の記事ファイルを見つける

サポート技術情報（KB）では、記事はセクションに整理され、カテゴリの下にネストされています。

例えば、[AdobeMagentoステータスのアップデートを購読する方法 ](/help/how-to/general/how-to-subscribe-to-adobe-magento-status-updates.md) 記事は、「方法」カテゴリの「一般」セクションに属しています。

記事ページのパンくずリストのパスに、セクションとカテゴリ名が表示されます。次の画像を参照してください。

![ カテゴリおよびセクションのパンくずリスト ](assets/breadcrumbs.png)

記事ファイルは、[magento/knowledge-base](https://github.com/magento/knowledge-base) リポジトリと同じ方法で整理されます。
すべてのコンテンツは `src` フォルダーに保存されます。カテゴリのフォルダーとセクションのネストされたフォルダーがあります。ファイル名は、記事のタイトルと一致するか、類似しています。

サポート技術情報の記事のテキストを検索文字列として使用して、リポジトリ内で検索を使用することもできます。 この文字列を含むファイルが検索結果に返されたら、必ず適切なセクションとカテゴリに属するファイルを選択してください。

### 貢献度ポイント

[magento/knowledge-base](https://github.com/magento/knowledge-base) リポジトリは、コントリビューションポイントとサポートのためにMagentoのコミュニティエンジニアリングと統合されています。

ポイントの付与方法については、[ 投稿ポイント ](https://github.com/magento/knowledge-base/blob/main/docs/contribution-points.md) ドキュメントを参照してください。
