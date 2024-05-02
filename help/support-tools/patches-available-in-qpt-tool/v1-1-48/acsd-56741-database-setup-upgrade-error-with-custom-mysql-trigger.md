---
title: 「ACSD-56741：カスタム MySQL トリガーを使用したデータベース設定エラーのトラブルシューティング」
description: ACSD-56741 パッチを適用すると、「setup:upgrade」の間に、インデックス化およびAdobe Commerceに関連しないデータベースのカスタム MySQL トリガーにより、「null 型の値で配列オフセットにアクセスしようとしています」というエラーメッセージが表示される AEM の問題を修正できます。 [!DNL MView].
feature: Install
role: Admin, Developer
source-git-commit: 216ce1035584e4c049029073ee0017d3616cdbd6
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# ACSD-56741：カスタム MySQL トリガーを使用したデータベース設定エラーのトラブルシューティング

ACSD-56741 パッチは、エラーメッセージが表示される問題を修正します *型 null の値の配列オフセットにアクセスしようとしています* 表示期間 `setup:upgrade` インデックス化に関連しないデータベース内のカスタム MySQL トリガーが原因で、および [!DNL MView]. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされています。 パッチ ID は ACSD-56741 です。 この問題はAdobe Commerce 2.5.0 で修正される予定です

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

エラーメッセージ *型 null の値の配列オフセットにアクセスしようとしています* 表示期間 `setup:upgrade` インデックス化に関連しないデータベース内のカスタム MySQL トリガーが原因で、および [!DNL MView].

<u>再現手順</u>:

1. 実行 `php bin/magento indexer:set-mode schedule`.

   ```
   DELIMITER //
   CREATE TRIGGER trg_catalog_category_entity_before_delete_umis BEFORE DELETE ON catalog_category_entity FOR EACH ROW
       -> BEGIN
       -> UPDATE ewave_navigation_menu_item_info as nit INNER JOIN ewave_navigation_menu_category_type as ncmi ON nit.id = ncmi.menu_item_id AND ncmi.category_id = OLD.entity_id SET nit.status = 0;
       -> END //
   ```

1. 実行 `php bin/magento c:f`.
1. 実行 `php bin/magento setup:upgrade`.

<u>期待される結果</u>:

セットアップのアップグレードはエラーなしで完了します。

<u>実際の結果</u>:

セットアップのアップグレードが終了し、次のエラーメッセージが表示されます。

*警告：null 型の値の配列オフセットにアクセスしようとしています*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
