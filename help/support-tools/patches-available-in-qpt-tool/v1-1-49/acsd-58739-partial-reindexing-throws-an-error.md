---
title: 「ACSD-58739：部分的なインデックス再作成でエラーがスローされる」
description: ACSD-55241 パッチを適用して、部分的なインデックス再作成がエラーをスローするAdobe Commerceの問題を修正してください。
feature: Inventory, Products
role: Admin, Developer
source-git-commit: b21eab3bf8ec492f0b1c5be9c13c6c579f43fe44
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# ACSD-58739：部分的なインデックス再作成でエラーがスローされる

ACSD-58739 パッチでは、部分的なインデックス再作成でエラーがスローされる問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.49 がインストールされている場合に使用できます。 パッチ ID は ACSD-58739 です。 この問題はAdobe Commerce 2.4.8 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.7

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.7 ～ 2.4.8

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

部分的なインデックス再作成はエラーをスローします。

<u> 再現手順 </u>:

1. `app/etc/ev.php` にスレーブ接続設定を追加します。
1. 最大 10000 個の製品を生成し、次のコマンドを実行します。

   ```
   bin/magento index:reindex
   ```

1. 生成された製品 ID を DB テーブル `catalogsearch_fulltext_cl` 追加します。

   ```
   insert into catalogsearch_fulltext_cl (entity_id) select entity_id from catalog_product_entity;
   ```

1. 次のコマンドを実行して、部分再インデックスをトリガーにします。

   ```
   bin/magento cron:run --group=index --bootstrap=standaloneProcessStarted=1 
   ```

1. `var/log/support_report.log` ファイルを確認します。

<u> 期待される結果 </u>

エラーはありません。

<u> 実際の結果 </u>:

*ベース テーブルまたはビューが見つかりません* 部分的なインデックス再作成の実行時にエラーが発生します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
