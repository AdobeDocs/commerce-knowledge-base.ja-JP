---
title: 「ACSD-48366：メールテンプレートに製品画像 [!UICONTROL Back to Stock] 表示されない」
description: ACSD-48366 パッチを適用すると、製品の在庫通知メールに製品のサムネール画像が表示されないAdobe Commerceの問題を修正できます。
exl-id: 57b549b0-6e97-4d5f-927e-9585f3257872
feature: Admin Workspace, Communications, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# ACSD-48366：メールテンプレートに製品画像 [!UICONTROL Back to Stock] 表示されない

ACSD-48366 パッチは、製品の在庫通知メールに製品のサムネール画像が表示されない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされている場合に使用できます。 パッチ ID は ACSD-48366 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

商品画像は [!UICONTROL Back to Stock] メールテンプレートには表示されません。

<u> 再現手順 </u>:

1. **[!UICONTROL Store]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Product Alert]**/**[!UICONTROL Allow Alert When Product Comes Back in Stock]**=*[!UICONTROL Yes]* に移動して、*[!UICONTROL Back in Stock]* の *[!UICONTROL Product Alert]* を有効にします。
1. **[!UICONTROL Store]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Inventory]**/**[!UICONTROL Display Out of Stock]**=*[!UICONTROL Yes]* に移動して、*[!UICONTROL Display Out of Stock Products]* を有効にします。
1. 数量= 0 の単純製品を作成します。
1. ストアフロントから顧客を作成し、上記の製品を購読して、在庫がある場合に製品アラートを取得します。
1. 商品を在庫にしてください。
1. 製品アラート cron を実行します。

   ```
   n98-magerun2.phar sys:cron:run catalog_product_alert
   ```

1. 顧客の製品アラートを開始します。

   ```
   bin/magento queue:consumers:start product_alert
   ```

1. メールを確認します。 在庫アラートメールがメールキャッチャーで使用できるようになりました。

<u> 期待される結果 </u>:

商品画像は、在庫アラートメールに表示されます。

<u> 実際の結果 </u>:

在庫通知メールに製品画像は表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
