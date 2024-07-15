---
title: 「ACSD-57337：アクセス制限を持つ管理者ユーザーが、*会社* グリッドのすべての会社を表示できる」
description: ACSD-57337 パッチを適用すると、特定の web サイトへのアクセス制限を持つ管理者ユーザーが*会社* グリッドのすべての web サイトの会社を表示できるAdobe Commerceの問題を修正できます。
feature: Companies, B2B, Configuration
role: Admin, Developer
exl-id: e49289a1-fe86-42b7-8d93-71f35b5e318d
source-git-commit: 33a9cb0227b318a0fff135621ecd6642f2fa827a
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# ACSD-57337：アクセス制限を持つ管理者ユーザーが、*会社* グリッド内のすべての会社を表示できる

ACSD-57337 パッチは、特定の web サイトへのアクセス制限を持つ管理者ユーザーが *会社* グリッド内のすべての web サイトの会社を表示できる問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされている場合に使用できます。 パッチ ID は ACSD-57337 です。 この問題はAdobe Commerce 2.5.0 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

特定の web サイトへのアクセス制限を持つ管理者ユーザーは、*会社* グリッド内のすべての web サイトの会社を表示できます。

<u> 再現手順 </u>:

1. 追加の web サイトを作成し、保存およびレビューします。
1. 異なる web サイトに割り当てられている会社をいくつか作成します。
1. 管理者ユーザーロールを作成し、作成した web サイトにロール範囲を設定します。
1. 管理者を作成し、作成した役割に割り当てます。
1. 新しい管理者でログインします。
1. **[!UICONTROL Customers]**/**[!UICONTROL Companies]** を開き、会社のリストを確認します。

<u> 期待される結果 </u>:

追加の web サイトに割り当てられている会社が *会社* グリッドに表示されます。

<u> 実際の結果 </u>:

すべての会社が *会社* グリッドに表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
