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

ACSD-56621 パッチでは、会社の管理者ユーザーの更新された名と姓が「挨拶ヘッダー」セクションに反映されない問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.46 がインストールされている場合に使用できます。 パッチ ID は ACSD-56621 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

更新された名前は、会社の管理者ユーザーの挨拶ヘッダーには表示されません。

<u> 再現手順 </u>:

1. **[!UICONTROL Admin]** パネルに移動します。
1. **[!UICONTROL Stores]** に移動し、「**[!UICONTROL Configuration]**」を選択します。
1. 「**[!UICONTROL General]**」セクションで、「**[!UICONTROL B2B]**」を選択して、B2B 会社の機能を有効にします。
1. **[!UICONTROL Storefront]** に移動して、新しい会社を登録してください。
1. 会社管理者ユーザーとしてログインします。
1. **[!UICONTROL My Account]**/**[!UICONTROL Company Users]** に移動し、必要に応じて「名」フィールドと「姓」フィールドを変更します。

<u> 期待される結果 </u>:

挨拶ヘッダーセクションのユーザーの姓と名は、すぐに変更されます。

<u> 実際の結果 </u>:

ユーザーの姓と名は、ユーザーがログアウトして再度ログインした場合にのみ変更されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
