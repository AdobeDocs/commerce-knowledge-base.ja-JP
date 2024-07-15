---
title: 「ACSD-56741：カスタム MySQL トリガーを使用したデータベース設定エラーのトラブルシューティング」
description: ACSD-56741 パッチを適用すると、「setup:upgrade」の間、インデックスおよび  [!DNL MView] に関連しないデータベース内のカスタム MySQL トリガーが原因で、「null 型の値で配列オフセットにアクセスしようとしています」というエラーメッセージが表示されるAdobe Commerceの問題を修正できます。
feature: Install
role: Admin, Developer
exl-id: 97839140-03c5-44f0-ba75-935d62f5bf90
source-git-commit: 7cd830d9ba4af6350a14e0cdb50439d2d07084dc
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# ACSD-56741：カスタム MySQL トリガーを使用したデータベース設定エラーのトラブルシューティング

ACSD-56741 パッチでは、インデックスおよび [!DNL MView] に関連しないデータベース内のカスタム MySQL トリガーが原因で、`setup:upgrade` 行中にエラーメッセージ *null 型の値で配列オフセットにアクセスしようとしています* が表示される問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされている場合に使用できます。 パッチ ID は ACSD-56741 です。 この問題はAdobe Commerce 2.5.0 で修正される予定です

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

インデックスおよび [!DNL MView] に関連しないデータベース内のカスタム MySQL トリガーが原因で、`setup:upgrade` 行中にエラーメッセージ *型 null の値で配列オフセットにアクセスしようとしています* が表示されます。

<u> 再現手順 </u>:

1. `php bin/magento indexer:set-mode schedule` を実行します。

   ```
   DELIMITER //
   CREATE TRIGGER trg_catalog_category_entity_before_delete_umis BEFORE DELETE ON catalog_category_entity FOR EACH ROW
       -> BEGIN
       -> UPDATE ewave_navigation_menu_item_info as nit INNER JOIN ewave_navigation_menu_category_type as ncmi ON nit.id = ncmi.menu_item_id AND ncmi.category_id = OLD.entity_id SET nit.status = 0;
       -> END //
   ```

1. `php bin/magento c:f` を実行します。
1. `php bin/magento setup:upgrade` を実行します。

<u> 期待される結果 </u>:

セットアップのアップグレードはエラーなしで完了します。

<u> 実際の結果 </u>:

セットアップのアップグレードが終了し、次のエラーメッセージが表示されます。

*警告：null 型の値の配列オフセットにアクセスしようとしています*。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
