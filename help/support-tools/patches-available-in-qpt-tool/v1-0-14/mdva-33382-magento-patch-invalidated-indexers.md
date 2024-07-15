---
title: 'MDVA-33382 パッチ：無効なインデクサー'
description: MDVA-33382 パッチは、カテゴリ内の製品を追加、削除、または並べ替えた後にインデクサーが無効化される問題を解決します。 無効化されるインデクサーは、「catalog_category_product」、「catalogsearch_fulltext」（およびその依存関係）です。
exl-id: b4ac10ee-0f9d-4d7a-be72-c4d90ebadb10
feature: Catalog Management, Categories, Price Indexer
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# MDVA-33382 パッチ：無効化されたインデクサー

MDVA-33382 パッチは、カテゴリ内の製品を追加、削除、または並べ替えた後にインデクサーが無効化される問題を解決します。 無効になるインデクサーは、`catalog_category_product`、`catalogsearch_fulltext` （およびその扶養家族）です。

このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.14 がインストールされている場合に使用できます。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.3.0～2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. すべてのインデクサーモードを **スケジュールに従って更新** に設定します。
1. カテゴリ編集ページから製品を削除します。
1. カテゴリの保存。
1. バックエンドまたは CLI でインデックスのステータスを検証します。

<u> 期待される結果 </u>:

`catalog_category_product`、`catalogsearch_fulltext` （およびその扶養家族）のインデックスは期待どおりに無効化されません。

<u> 実際の結果 </u>:

`catalog_category_product`、`catalogsearch_fulltext` （およびその扶養家族）のインデックスが無効になります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
