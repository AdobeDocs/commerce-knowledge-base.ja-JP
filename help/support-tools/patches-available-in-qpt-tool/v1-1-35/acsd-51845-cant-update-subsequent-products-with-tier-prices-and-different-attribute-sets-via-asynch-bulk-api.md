---
title: 「ACSD-51845：非同期一括を使用して、階層価格と異なる属性セットで後続の製品を更新できない [!DNL API]“
description: ACSD-51845 パッチを適用すると、階層価格や異なる属性セットを使用して後続の製品を非同期バルクで更新できないAdobe Commerceの問題を修正できます [!DNL REST API].
feature: REST, Products
role: Admin
exl-id: c3fff9f2-30ad-4bcb-945e-e9e0c69630b3
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# ACSD-51845：非同期一括を使用して、階層価格と異なる属性セットで後続の製品を更新できない [!DNL API]

ACSD-51845 パッチを適用すると、非同期バルクを使用して階層価格と異なる属性セットで後続の製品を更新できない問題が修正されます [!DNL REST API]. このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-51845 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

階層価格と異なる属性セットを持つ後続の製品の更新が、非同期バルクを介して失敗する [!DNL REST API].

<u>再現手順</u>:

1. 設定 [!DNL RabbitMQ].
1. 2 つの属性セットを作成します。
1. 2 つ作成 **シンプル製品**、各製品を異なる属性セットに割り当てます。
1. を追加 **顧客グループ価格** 製品ごとに調整します。
1. 両方の製品を同じ一括更新 [!DNL API] 更新。
1. 次のことを確認します `bin/magento queue:consumers:start async.operations.all` コマンドを実行中です。
1. 一括で確認 [!DNL API] ステータス。

<u>期待される結果</u>:

サービスが正常に実行されました。

<u>実際の結果</u>:

次のエラーメッセージが返されます。 *商品を保存できませんでした。 もう一度やり直してください。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
