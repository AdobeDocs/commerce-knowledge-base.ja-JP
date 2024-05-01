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

MDVA-33382 パッチは、カテゴリ内の製品を追加、削除、または並べ替えた後にインデクサーが無効化される問題を解決します。 無効化されるインデクサーは次のとおりです `catalog_category_product` , `catalogsearch_fulltext` （およびその扶養家族）。

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.14 がインストールされています。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. すべてのインデックスモードをに設定 **スケジュールに従って更新**.
1. カテゴリ編集ページから製品を削除します。
1. カテゴリの保存。
1. バックエンドまたは CLI でインデックスのステータスを検証します。

<u>期待される結果</u>:

次のインデックスは無効化されません。 `catalog_category_product` , `catalogsearch_fulltext` （およびその扶養家族）の要件は予想通りです。

<u>実際の結果</u>:

次のインデックスが無効になります。 `catalog_category_product` , `catalogsearch_fulltext` （およびその扶養家族）。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
