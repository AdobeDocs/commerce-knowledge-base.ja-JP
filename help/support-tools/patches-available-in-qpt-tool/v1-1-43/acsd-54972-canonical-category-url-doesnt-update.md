---
title: 「ACSD-54972：正規カテゴリ URL が更新されない」
description: カテゴリ URL を変更した後、正規カテゴリ URL が更新されないAdobe Commerceの問題を修正するために、ACSD-54972 パッチを適用してください。
feature: Catalog Management, Products, Categories
role: Admin, Developer
exl-id: 2d78f5f6-d485-45a4-a40d-9a0ddd124f82
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# ACSD-54972：正規カテゴリ URL が、カテゴリ URL の変更後に更新されない

ACSD-54972 パッチは、カテゴリ URL を変更した後、正規カテゴリ URL が更新されない問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされています。 パッチ ID は ACSD-54972 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カテゴリ URL を変更した後、正規カテゴリ URL が更新されない。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Catalog]** > **[!UICONTROL Search Engine Optimization]**.

   * を設定 *[!UICONTROL Use Canonical Link Meta Tag for Categories]*: *はい*

2. カテゴリを作成します（例：）。 *名前*: *カテゴリ 01*, *URL キー*: *カテゴリ–01*）に設定します。
3. を更新 *URL キー* 元の値と異なるものへの保持 **[!UICONTROL Create Permanent Redirect for old URL]** チェックボックスがオンになっています。
4. キャッシュをクリーンアップします。
5. に移動します *[!UICONTROL Category Page]* フロントエンドで。
6. ページソースを確認し、 *正規* タグ。

<u>期待される結果</u>:

`<link rel="canonical" href="http://127.0.0.1/pub/category-01-new.html" />`

<u>実際の結果</u>:

`<link rel="canonical" href="http://127.0.0.1/pub/category-01.html" />`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
