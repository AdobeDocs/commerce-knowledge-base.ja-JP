---
title: 「ACSD-49849：顧客の電子メールが PayPal の電子メールに置き換えられた」
description: GraphQL経由で PayPal Express で注文する際に、お客様のメールが PayPal メールに置き換わっていたAdobe Commerceの問題を修正するために、ACSD-49849 パッチを適用します。
exl-id: 826ea90a-ac10-43e8-aa88-bd69b152ded8
feature: Admin Workspace, Communications, Orders, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# ACSD-49849：顧客の電子メールがに置き換えられる [!DNL PayPal] 電子メール

ACSD-49849 パッチは、顧客の電子メールが [!DNL PayPal's] で注文する際のメール [!DNL PayPal Express] GraphQL経由 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされています。 パッチ ID は ACSD-49849 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.5-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

顧客の電子メールがに置き換えられます [!DNL PayPal's] で注文する際のメール [!DNL PayPal Express] GraphQL経由

<u>再現手順</u>:

1. に移動 **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Payments]**.
1. の有効化と設定 [!DNL PayPal Express] およびを設定 **[!UICONTROL Payment Action]** = **[!UICONTROL Sale]**.
1. に移動 **[!UICONTROL Catalog]** > **[!UICONTROL Products]**&#x200B;シンプルな製品を作成します。
1. GraphQLを使用してゲストのチェックアウトを完了します。 詳しくは、 [GraphQLのチェックアウトチュートリアル](https://developer.adobe.com/commerce/webapi/graphql/tutorials/checkout/) （Adobe Commerce開発者向けドキュメント）を参照してください。
1. 使用方法 [!DNL PayPal Express] 支払方法として。
1. 次の手順で使用したメールをメモします [買い物かごに関するメールの設定](https://developer.adobe.com/commerce/webapi/graphql/tutorials/checkout/set-email-address/) （Adobe Commerce開発者向けドキュメント）を参照してください。
1. 注文したら、Adobe Commerce管理者に移動し、作成した注文のメールを確認します。

<u>期待される結果</u>:

メールは、チェックアウト時に設定されたものと同じです。

<u>実際の結果</u>:

チェックアウト中のメールセットは、内のメールセットによって上書きされます。 [!DNL PayPal] アカウント。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
