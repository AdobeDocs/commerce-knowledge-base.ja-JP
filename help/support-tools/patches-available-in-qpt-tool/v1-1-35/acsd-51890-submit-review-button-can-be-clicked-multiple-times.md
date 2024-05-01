---
title: 'ACSD-51890: [!UICONTROL Submit review] ボタンは複数回クリックできます'
description: Adobe Commerce ACSD-51890 パッチを適用して、 [!UICONTROL Submit Review] ボタンは、次の操作を行わずに複数回クリックできます [!DNL Google reCAPTCHA v3] 検証。
feature: Products
role: Admin
exl-id: f6369a24-24bd-4e5e-a870-a13f507ada94
source-git-commit: 7dbf9a796fe2026b0657b719d10e5bb21b964fb6
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# ACSD-51890: **[!UICONTROL Submit Review]** ボタンは、次の操作を行わずに複数回クリックできます **[!DNL Google reCAPTCHA v3]** 検証

>[!NOTE]
>
>このパッチはに置き換えられます [ACSD-55112](/help/support-tools/patches-available-in-qpt-tool/v1-1-42/acsd-55112-submit-review-button-can-be-clicked-multiple-times.md).

ACSD-51890 パッチは、 **[!UICONTROL Submit Review]** ボタンは、次の操作を行わずに複数回クリックできます **[!DNL Google reCAPTCHA v3]** 検証。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.35 がインストールされています。 パッチ ID は ACSD-51890 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この **[!UICONTROL Submit Review]** ボタンは、 **[!DNL Google reCAPTCHA v3]** 検証。

<u>再現手順</u>:

1. Enable （有効） **[!DNL Google reCAPTCHA v3]** 製品レビュー用
1. 製品ページを開き、に移動します。 **[!UICONTROL Review]** を選択し、 [!DNL reCAPTCHA] 表示されています。
1. レビューフォームに入力し、 **[!UICONTROL Submit Review]** できるだけ早く、複数回ボタンを押します。
1. を開きます **[!UICONTROL Review]** 管理者からのセクション。

<u>期待される結果</u>

重複するレビューは作成されません。

<u>実際の結果</u>

重複するレビューが作成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
