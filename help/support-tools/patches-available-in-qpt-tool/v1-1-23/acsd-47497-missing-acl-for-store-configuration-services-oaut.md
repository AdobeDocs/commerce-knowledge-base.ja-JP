---
title: 「ACSD-47497：ストア/設定/サービス [!UICONTROL OAuth] ードの ACL がありません」
description: 特定の役割に権限が設定されており、設定セクションへのアクセスを定義できない場合は、ACSD-47497 パッチを適用して、Adobe Commerceの問題を修正してください。
exl-id: c13fd541-1379-4893-9190-9da1422b2b99
feature: Configuration, Identity Management, Services
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# ACSD-47497：ストア/設定/サービス [!UICONTROL OAuth] の ACL がありません

ACSD-47497 パッチを使用すると、Adobe Commerce Admin の **[!UICONTROL Configuration]** セクションに「**[!UICONTROL Services]**」タブが表示されない問題を解決できます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.23 がインストールされている場合に使用できます。 パッチ ID は ACSD-47497 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

特定の役割に対して権限が設定されている場合、**[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Services]**/**[!UICONTROL OAuth]** へのアクセスを定義することはできません。

<u> 再現手順 </u>:

1. Adobe Commerce Admin にログインします。 **[!UICONTROL System]**/**[!UICONTROL Permissions]**/**[!UICONTROL User Roles]** に移動します。
1. 管理者の役割で「**[!UICONTROL Role Resources]**」を選択し、「**[!UICONTROL Roles Resources]**」の下の「**[!UICONTROL Resource Access]**」を「_カスタム_」に設定して、すべてのチェックボックスをオンにします。 「**[!UICONTROL Save Role]**」を選択します。
1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Services]** を選択します。 **[!UICONTROL OAuth]** 設定セクションは使用できません。

<u> 期待される結果 </u>:

**[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Services]**/**[!UICONTROL OAuth]** に、設定セクションが表示されます。

<u> 実際の結果 </u>:

**[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Services]**/**[!UICONTROL OAuth]** に、設定セクションがありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
