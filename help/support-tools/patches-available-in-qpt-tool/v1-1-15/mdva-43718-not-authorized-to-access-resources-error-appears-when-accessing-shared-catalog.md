---
title: 「MDVA-43718：共有カタログにアクセスすると、「コンシューマーはリソースへのアクセスを許可されていません」エラーが表示される」
description: MDVA-43718 パッチは、エラー*consumer が %resources へのアクセスを許可されていない問題を解決します。*は、カスタム統合から共有カタログにアクセスすると表示されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.15 がインストールされている場合に利用できます。 パッチ ID は MDVA-43718。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: fa783ed4-906e-4ee6-b82a-cfe6db5ae89e
feature: Catalog Management
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# MDVA-43718：共有カタログにアクセスすると、「コンシューマーはリソースへのアクセスを許可されていません」というエラーが表示される

MDVA-43718 パッチを適用すると、エラーが発生する問題が解決されます *コンシューマーは %resources へのアクセスを許可されていません。* カスタム統合から共有カタログにアクセスすると表示されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.15 がインストールされています。 パッチ ID は MDVA-43718。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カスタム統合から共有カタログにアクセスすると、次のエラーが表示されます。 *コンシューマーは %resources へのアクセスを許可されていません*.

<u>再現手順</u>:

1. 管理者/から新しい統合を作成 **システム** > **統合** > **統合を追加**.
1. 次のリソースへのアクセスを追加し、統合を有効化します。

   * Magento_SharedCatalog::list
   * Magento_SharedCatalog::manage
   * Magentoカタログ：:catalog

1. 統合アクセスの使用： `rest/default/V1/sharedCatalog/1`

<u>期待される結果</u>:

共有カタログの詳細が返されます。

<u>実際の結果</u>:

次のエラーが返されます。

```JSON
"message": "The consumer isn't authorized to access %resources.",
"resources": "Magento_SharedCatalog::sharedCatalog"
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
