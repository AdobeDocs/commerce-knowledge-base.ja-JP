---
title: 「ACSD-53347：価格インデックス作成のパフォーマンスが時間とともに徐々に低下」
description: ACSD-53347 パッチを適用すると、大規模な商品カタログのインデックスを再作成する際にパフォーマンスが徐々に低下するAdobe Commerceの問題を修正できます。
feature: Price Indexer
role: Admin
exl-id: 28795673-54b0-4282-bd43-344401cbe140
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# ACSD-53347：価格インデックス作成のパフォーマンスが時間とともに徐々に低下

ACSD-53347 パッチは、大規模な製品カタログの価格のインデックスを再作成するとパフォーマンスが徐々に低下する問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.38 がインストールされている場合に使用できます。 パッチ ID は ACSD-53347 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

大規模な製品カタログの価格のインデックスを再作成すると、インデックス作成プロセス中に実行されるクエリのパフォーマンスが徐々に低下します。

<u> 再現手順 </u>:

1. 大きなシンプルなカタログを作成し、これらの製品にカスタムオプションを割り当てます（カスタムオプションでは、インデックス作成時に一時テーブルを使用します）。
1. 少なくとも 200 以上の顧客グループを作成して、イシューの可視性を高めます。
1. 10 以上の web サイトを作成し、それぞれに製品をすべて割り当てます。
1. 読み込まれる製品はほぼ同じで、SKU と名前のみが異なります。
1. **[!UICONTROL DB Logging]** を有効にします。
1. `bin/magento index:reindex catalog_product_price` コマンドを実行します。
1. `db.log` で `catalog_product_index_price_opt_agr_temp`*から* DELETEを確認してください。

<u> 期待される結果 </u>:

*DB クエリ* の実行は効率的に行われます。

<u> 実際の結果 </u>:

一時テーブルに対する *DB クエリ* のパフォーマンスが長時間遅くなるため、価格インデックス作成テーブルの完了に多くの時間がかかります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
