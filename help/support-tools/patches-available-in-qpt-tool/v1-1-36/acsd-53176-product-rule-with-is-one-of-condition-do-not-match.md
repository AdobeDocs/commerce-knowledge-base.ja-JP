---
title: 「ACSD-53176:「次の 1 つ」条件を含む製品ルールが一致しません」
description: ACSD-53176 パッチを適用すると、関連する商品ルールの「is one of」条件が「Products to Match」で正しく機能しないAdobe Commerceの問題を修正できます。
feature: Marketing Tools
role: Admin
exl-id: 91f05f5b-6a5e-4b93-9dfb-88cbeccb6c9e
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# ACSD-53176：製品ルールと `is one of` 条件が一致しません

ACSD-53176 パッチは、関連する製品ルールが `is one of` の条件が正しく機能しません **一致する製品**. このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.36 がインストールされています。 パッチ ID は ACSD-53176 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.5-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

関連する製品ルール `is one of` の条件が正しく機能しません **一致する製品**.

<u>再現手順</u>:

1. 3 ～ 4 個の製品を作成します。
1. 新しい関連製品ルールを作成します。

   複数の製品に一致するルールを設定します。
   * `SKU is one of "S1,S2".`

   2 つ以上の項目を表示するようにルールを設定します。
   * `Product SKU is one of constant value "S2,S3".`

1. ストアフロントで S1 製品を開きます。

<u>期待される結果</u>:

関連製品「S2」、「S3」を製品ページ「S1」、「S2」の両方に表示する。

<u>実際の結果</u>:

関連製品が製品ページに表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
