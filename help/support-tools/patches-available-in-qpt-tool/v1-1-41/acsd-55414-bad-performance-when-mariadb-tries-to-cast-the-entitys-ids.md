---
title: 「ACSD-55414:MariaDB が entitys_ids をキャストしようとすると、パフォーマンスが低下します」
description: MariaDB が「entitys_ids」を文字列から整数に変換しようとすると、インデックス再作成のパフォーマンスが妨げられ、Adobe Commerceの問題を修正するために ACSD-55414 パッチを適用してください。
feature: Attributes
role: Admin, Developer
exl-id: 008a4fda-5d80-47e2-8fb4-c1e39d15a6ba
source-git-commit: 35cd21581ee34a6213be42a79e159439b8856fb6
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# ACSD-55414:MariaDB が `entitys_ids` をキャストしようとすると、パフォーマンスが低下します

ACSD-55414 パッチでは、MariaDB が `entitys_ids` を文字列から整数に変換しようとすると、インデックス再作成のパフォーマンスが妨げられる問題が修正されています。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.41 がインストールされている場合に使用できます。 パッチ ID は ACSD-55414 です。 この問題はAdobe Commerce 2.4.6 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

MariaDB が `entitys_ids` を文字列から整数にキャストしようとすると、インデックス再作成のパフォーマンスが妨げられます。

<u> 再現手順 </u>:

1. *50000* の簡単な製品を設定して `setup/performance-toolkit/profiles/ce/small.xml` を更新します。
1. コマンド `bin/magento setup:perf:generate-fixtures setup/performance-toolkit/profiles/ce/small.xml` を実行して、このプロファイルを生成します。
1. 再インデックス（`bin/magento indexer:reindex catalog_product_attribute`）を実行します。

<u> 期待される結果 </u>:

再インデックスの完了には十分な時間がかかります。

<u> 実際の結果 </u>:

この再インデックスの完了に時間がかかりすぎます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
