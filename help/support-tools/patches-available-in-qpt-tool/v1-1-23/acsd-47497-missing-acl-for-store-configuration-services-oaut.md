---
title: 「ACSD-47497：ストア/設定/サービスの ACL がありません [!UICONTROL OAuth]'
description: 特定の役割に権限が設定されており、設定セクションへのアクセスを定義できない場合は、ACSD-47497 パッチを適用して、Adobe Commerceの問題を修正してください。
exl-id: c13fd541-1379-4893-9190-9da1422b2b99
feature: Configuration, Identity Management, Services
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# ACSD-47497：ストア/設定/サービスの ACL がありません [!UICONTROL OAuth]

ACSD-47497 パッチは、 **[!UICONTROL Services]** でタブが表示されない **[!UICONTROL Configuration]** Adobe Commerce Admin の「」セクション。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.23 がインストールされています。 パッチ ID は ACSD-47497 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

特定の役割用に権限が設定されている場合、へのアクセスを定義することはできません **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL OAuth]**.

<u>再現手順</u>:

1. Adobe Commerce Admin にログインします。 に移動 **[!UICONTROL System]** > **[!UICONTROL Permissions]** > **[!UICONTROL User Roles]**.
1. を選択 **[!UICONTROL Role Resources]** 管理者ロールで、を設定します **[!UICONTROL Resource Access]** 未満 **[!UICONTROL Roles Resources]** 対象： _カスタム_&#x200B;次に、すべてのチェックボックスをオンにします。 を選択 **[!UICONTROL Save Role]**.
1. を選択 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]**. この **[!UICONTROL OAuth]** 設定セクションは使用できません。

<u>期待される結果</u>:

対象： **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL OAuth]**&#x200B;の場合、設定セクションが表示されます。

<u>実際の結果</u>:

対象： **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL OAuth]**、設定セクションがありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
