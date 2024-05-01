---
title: 「ACSD-51240：会社登録フォームでの登録中に、アップロードしたファイルが見つからない」
description: ACSD-51240 パッチを適用すると、会社登録フォーム経由での登録時に、アップロードしたファイルが見つからないAdobe Commerceの問題を修正できます。
exl-id: e5822c54-4e77-46b0-84b6-5e25c3845974
source-git-commit: e1fe8936c56f422ae591c6424d8a72621093db81
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# ACSD-51240：会社登録フォーム経由での登録中に、アップロードしたファイルが見つからない

>[!NOTE]
>
>このパッチはに置き換えられます [ACSD-55628](/help/support-tools/patches-available-in-qpt-tool/v1-1-42/acsd-55628-upload-file-company-registration-form-replace-file-customer-attribute-storefront.md).

ACSD-51240 パッチは、会社登録フォーム経由で登録する際に、アップロードしたファイルが見つからない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされています。 パッチ ID は ACSD-51240 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 &lt; 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>). この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 問題

アップロード済みファイルが、会社登録フォーム経由での登録中に見つかりません。

<u>再現手順</u>:

1. を設定 **[!UICONTROL Admin]** > **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL General]** > **[!UICONTROL B2B >Company]** > **[!UICONTROL Enable]** = *はい*.
1. の新しい顧客属性を作成 **[!UICONTROL File]** タイプ、設定 **[!UICONTROL Show in StoreFront]** = *はい*&#x200B;を選択し、 **[!UICONTROL all forms]**.
1. ストアフロントで新しい会社を作成し、新しい属性の画像をアップロードします。
ストアフロントで会社と管理者ユーザーを開きます。

<u>期待される結果</u>:

アップロードされたファイルが表示されます。

<u>実際の結果</u>:

アップロードされたファイルは、の会社ページにも管理者の顧客ページにも表示されません。 [!UICONTROL Commerce Admin].

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
