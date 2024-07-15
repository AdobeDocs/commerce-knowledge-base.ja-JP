---
title: 「ACSD-54983：非アクティブなユーザーで、GraphQLを含む会社のユーザー UID を使用できない」
description: ユーザーステータスが非アクティブに設定されていると、GraphQL リクエストで会社のユーザー UID を取得できないAdobe Commerceの問題を修正するために、ACSD-54983 パッチを適用します。
feature: GraphQL
role: Admin, Developer
exl-id: 57e7b9ca-3421-4b50-86b4-abdf1b3d79d1
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# ACSD-54983：非アクティブなユーザーで、GraphQLを含む会社のユーザー UID を使用できない

ACSD-54983 パッチでは、ユーザーステータスが非アクティブに設定されている場合、GraphQL リクエストで会社のユーザー UID を取得できない問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされている場合に使用できます。 パッチ ID は ACSD-54983 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーステータスが非アクティブに設定されている場合、GraphQL リクエストで会社ユーザー UID を取得できない。

<u> 再現手順 </u>:

1. 管理者ユーザーで会社を作成します。 例：company@test.com
1. 顧客を新規作成します。
1. 新しい顧客を会社に割り当てます。
1. **[!UICONTROL company admin token]** を入手してください。
1. **[!UICONTROL company admin token]** を使用して、会社構造を取得します。 開発者向けドキュメントの [ 会社構造を返す ](https://developer.adobe.com/commerce/webapi/graphql/schema/b2b/company/queries/company/#return-the-company-structure) を参照してください。
1. 応答には、ID を持つ *アクティブ* 顧客のみが含まれます。
1. 会社ユーザーを *非アクティブ* に更新します。
1. 会社構造を再度取得します。

<u> 期待される結果 </u>:

ステータスが非アクティブに設定されている場合は、会社ユーザー UID を取得できます。

<u> 実際の結果 </u>:

非アクティブな顧客はリストに含まれていません。 ステータスが非アクティブに設定されている場合、会社ユーザー UID を取得できません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
