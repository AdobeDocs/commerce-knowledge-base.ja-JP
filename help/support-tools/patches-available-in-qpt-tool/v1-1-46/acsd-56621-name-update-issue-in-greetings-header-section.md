---
title: 「ACSD-56621：会社管理者ユーザーの挨拶ヘッダーに表示されない更新された名前」
description: ACSD-56621 パッチを適用すると、会社の管理者ユーザーの更新された名と姓が「挨拶ヘッダー」セクションに反映されないAdobe Commerceの問題が修正されます。
feature: Companies, B2B, User Account
role: Admin, Developer
exl-id: 4ad9c878-b617-4e6a-939c-be15faf7124b
source-git-commit: c5e94c6407394cd905ea470628d28db2c2c6c0ed
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# ACSD-56621：会社管理者ユーザーの挨拶ヘッダーに表示されない更新された名前

ACSD-56621 パッチでは、会社の管理者ユーザーの更新された名と姓が「挨拶ヘッダー」セクションに反映されない問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.46 がインストールされています。 パッチ ID は ACSD-56621 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

更新された名前は、会社の管理者ユーザーの挨拶ヘッダーには表示されません。

<u>再現手順</u>:

1. に移動します。 **[!UICONTROL Admin]** パネル。
1. に移動 **[!UICONTROL Stores]** を選択して、 **[!UICONTROL Configuration]**.
1. の下 **[!UICONTROL General]** セクションで選択 **[!UICONTROL B2B]** B2B 会社機能を有効にします。
1. に移動します **[!UICONTROL Storefront]** 新しい会社を登録します。
1. 会社管理者ユーザーとしてログインします。
1. に移動 **[!UICONTROL My Account]** > **[!UICONTROL Company Users]** を選択し、必要に応じて「名」フィールドと「姓」フィールドを変更します。

<u>期待される結果</u>:

挨拶ヘッダーセクションのユーザーの姓と名は、すぐに変更されます。

<u>実際の結果</u>:

ユーザーの姓と名は、ユーザーがログアウトして再度ログインした場合にのみ変更されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
