---
title: 「ACSD-53414：制限付き管理者ユーザーが、権限範囲外の CMS ページを表示できる」
description: ACSD-53414 パッチを適用すると、制限付き管理者ユーザーが権限適用範囲外の CMS ページを表示するAdobe Commerceの問題を修正できます。
feature: CMS
role: Admin, Developer
exl-id: f8540d52-a3bb-49bb-8868-7b1db03e571b
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# ACSD-53414：制限付き管理者ユーザーが、自身の権限範囲外の CMS ページを表示できる

ACSD-53414 パッチでは、制限付きの管理者ユーザーが、自身の権限範囲外の CMS ページを表示できる問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされています。 パッチ ID は ACSD-53414 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

制限付き管理者ユーザーは、権限範囲外の CMS ページも表示できます。

<u>再現手順</u>:

1. 新しい web サイト（sub_website）、ストア（sub_store）、ストレビュー（sub_storeview）を作成します。
1. sub_expert ロールを作成して、sub_website および sub_store の範囲を許可します。 次の権限のみを割り当てます。 [!UICONTROL Dashboard] および [!UICONTROL Pages].
1. 新しい管理者ユーザーを作成して、sub_expert ロールに割り当てます。
1. 以下の CSM ページを sub_storereview と default storereview に割り当てます。

   * [!UICONTROL 404 Not Found] > サブストレビュー
   * [!UICONTROL 503 Service Unavailable] > デフォルトの storreview

1. 手順 3 で作成した管理者ユーザーを使用して管理者にログインします。
1. CMS ページグリッドを確認します。

<u>期待される結果</u>:

*[!UICONTROL 503 Service Unavailable]* web 管理者にはページが表示されません。

<u>実際の結果</u>:

*[!UICONTROL 503 Service Unavailable]* web 管理者に表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
