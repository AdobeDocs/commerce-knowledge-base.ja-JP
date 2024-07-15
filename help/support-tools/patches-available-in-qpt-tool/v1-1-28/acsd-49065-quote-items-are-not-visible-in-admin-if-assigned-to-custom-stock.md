---
title: 「ACSD-49065：引用符項目が管理者に表示されない」
description: ACSD-49065 パッチを適用すると、見積もり品目がカスタム在庫にのみ割り当てられている場合に管理者に表示されないAdobe Commerceの問題を修正できます。
exl-id: 3a5ceb4c-4c94-4938-98d9-9171f2633056
feature: Admin Workspace, B2B, Orders, Quotes
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# ACSD-49065：引用符項目が管理者に表示されない

ACSD-49065 パッチは、見積もり項目がカスタムストックにのみ割り当てられている場合に管理者に表示されない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされている場合に使用できます。 パッチ ID は ACSD-49065 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

見積もり項目がカスタムストックにのみ割り当てられている場合、管理者に表示されません。

前提条件：

**[!UICONTROL B2B]** および **[!UICONTROL Inventory]** モジュールをインストールする必要があります。

<u> 再現手順 </u>:

1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL General]**/**[!UICONTROL B2B Features]** の下の **[!UICONTROL Company]** と **[!UICONTROL B2B Quote]** を有効にします。
1. セカンダリ **[!UICONTROL Inventory Source]** を作成し、セカンダリ **[!UICONTROL Inventory Stock]** に割り当てます。
1. セカンダリ（デフォルト以外）の **[!UICONTROL Inventory Source]** のみを割り当てて、新しい製品を作成します。
1. ストアフロントに移動し、新しい会社アカウントを作成します。 **[!UICONTROL Company Admin]** としてログインし、作成した商品を買い物かごに追加します。
1. 買い物かごに移動し、*[!UICONTROL Request a Quote]* します。
1. 管理者に移動し、**[!UICONTROL Sales]**/**[!UICONTROL Quotes]** で依頼された見積もりを表示します。

<u> 期待される結果 </u>:

商品を保存し直すことなく、新しい商品で作成された新しい見積もりに商品が表示される。

<u> 実際の結果 </u>:

*[!UICONTROL Items Quoted]* セクションは空です。 新しく作成した製品を再度保存すると、項目が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
