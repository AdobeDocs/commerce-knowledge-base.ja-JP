---
title: 「ACSD-55628：会社登録フォーム上のファイルをアップロードしています。ストアフロントの顧客属性用のファイルを置き換えています」
description: 会社登録フォームにファイルをアップロードし、ストアフロントの顧客属性のファイルを置き換えることで発生するAdobe Commerceの問題を修正するために、ACSD-55628 パッチを適用します。
feature: Storefront, Attributes, B2B, Customers
role: Admin, Developer
exl-id: ca85b459-f72b-4663-85af-1f793935fe7e
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# ACSD-55628：会社登録フォームへのファイルのアップロード、ストアフロントの顧客属性ファイルの置き換え

>[!NOTE]
>
>このパッチは、 [ACSD-51240](/help/support-tools/patches-available-in-qpt-tool/v1-1-33/acsd-51240-uploaded-file-missing-while-registering-via-company-registration-form.md).

ACSD-55628 パッチでは、会社登録フォームにファイルをアップロードし、ストアフロントの顧客属性のファイルを置き換える際の問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.42 がインストールされています。 パッチ ID は ACSD-55628 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2 &lt; 2.4.5 および 2.4.5-p1 &lt; 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアフロントで顧客属性のファイルを置き換えることができません。

<u>再現手順</u>:

1. 次の値を持つ新しい顧客属性を作成します。

   * *[!UICONTROL Input Type]*: *[!UICONTROL File (Attachment)]*
   * *[!UICONTROL Show on Storefront]*: *はい*
   * *[!UICONTROL Forms to Use In]*: *使用可能なすべてのオプション*

1. ストアフロントに顧客としてログインし、を開きます **[!UICONTROL My Account]** > **[!UICONTROL Account Information]**.
1. 新しい画像をアップロードして保存します。
1. ページを更新します。 古い画像を削除して、新しい画像をアップロードします。 変更を保存します。

<u>期待される結果</u>:

新しい画像が保存されます。

<u>実際の結果</u>:

古い画像は引き続き表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
