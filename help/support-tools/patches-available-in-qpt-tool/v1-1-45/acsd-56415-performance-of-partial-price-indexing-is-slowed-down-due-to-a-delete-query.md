---
title: 「ACSD-56415:「DELETE」クエリが原因で [!UICONTROL Partial Price Indexing] のパフォーマンスが低下しました」
description: ACSD-56415 パッチを適用すると、インデックスに部分的な価格データが多く含まれている場合に、「DELETE」クエリが原因で [!UICONTROL Partial Price Indexing] ータのパフォーマンスが低下するAdobe Commerceの問題を修正できます。
feature: Catalog Service
role: Admin, Developer
exl-id: 0b099570-9f27-4ae2-9384-6b69ea50bd98
source-git-commit: fe6269ac042326a85a2cab5ccf834ac3eff1c166
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# ACSD-56415：クエリが原因で [!UICONTROL Partial Price Indexing] のパフォーマンスが低下 `DELETE` る

ACSD-56415 パッチは、データベースに多くの部分価格データインデックスがある場合に、`DELETE` のクエリが原因で [!UICONTROL Partial Price Indexing] のパフォーマンスが低下する問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされている場合に使用できます。 パッチ ID は ACSD-56023 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

データベースに多くの部分価格データインデックスがある場合、`DELETE` のクエリが原因で [!UICONTROL Partial Price Indexing] のパフォーマンスが低下します。

<u> 再現手順 </u>:

1. 大規模なパフォーマンスプロファイルを使用して ** 300000 製品および *10 web サイト* 作成します。
1. 管理パネルにログインします。
1. *10 の顧客グループ* を作成します。
1. 次のクエリを実行して、`_cl` テーブルに製品を追加します。

   &grave;&grave;
    insert into catalog_product_price_cl (entity_id) select entity_id from catalog_product_entity
 &grave;&grave;

1. 次のコマンドを実行して、部分価格インデックス作成プロセスをトリガーします。

   &grave;&grave;
    bin/magento cron:run --group=index --bootstrap=standaloneProcessStarted=1
 &grave;&grave;

<u> 期待される結果 </u>:

SQL クエリDELETE`main_table` FROM `catalog_product_index_price` は迅速に実行されます。

<u> 実際の結果 </u>:

FROM `catalog_product_index_price` の SQL クエリDELETE`main_table` 実行に非常に時間がかかる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
