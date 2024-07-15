---
title: 'ACSD-55352：報酬ポイントを使用したクレジットメモの作成'
description: ACSD-55352 パッチを適用すると、顧客報酬ポイントを含む部分的なクレジットメモを作成した後、注文ステータスが「クローズ」に変わり、クレジットメモオプションが管理注文ページに表示されなくなるAdobe Commerceの問題を修正できます。
feature: Checkout, Orders
role: Admin, Developer
exl-id: 33ceb2e9-3cd5-4472-941a-e06c5c534f4a
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# ACSD-55352：報酬ポイントを使用したクレジットメモの作成

ACSD-55352 パッチでは、顧客報酬ポイントを含む部分的なクレジットメモを作成した後、注文ステータスが *クローズ* に変わり、クレジットメモオプションが管理注文ページから表示されなくなる問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.44 がインストールされている場合に使用できます。 パッチ ID は ACSD-55352 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

顧客報酬ポイントを含む部分的なクレジットメモを作成した後、注文ステータスが *クローズ* に変わり、クレジットメモオプションが管理注文ページから表示されなくなります。

<u> 再現手順 </u>:

1. Adobe Commerce Admin にログインします。
2. **[!UICONTROL Stores]**/**[!UICONTROL Other Setting]**/**[!UICONTROL Reward Exchange Rates]**/**[!UICONTROL Add New Rate]** に移動します。
3. 2 つの料率を追加します。
   * *[!UICONTROL First]*:
      * *[!UICONTROL Direction]* = *通貨を指します*
      * *[!UICONTROL Rate]* = *100*
      * *[!UICONTROL Upper Boundary]* = *100*
   * *[!UICONTROL Second]*:
      * *[!UICONTROL Direction]* = *通貨からポイント*
      * *[!UICONTROL Rate]* = *100*
      * *[!UICONTROL Upper Boundary]* = *100*
4. 価格が 100 *ドルで* 数量が *100* のシンプルな製品を作 *し* す。
5. ストアフロントから顧客を作成します。
6. バックエンドに再度アクセスします（**[!UICONTROL Customers]**/**[!UICONTROL All Customers]**/**[!UICONTROL Edit]**/**[!UICONTROL Reward Points]**/**[!UICONTROL Update Points]**/*100* を追加）。顧客を保存します。
7. ストアフロントに移動し、以前に作成した顧客としてログインします。
8. *数量* : *10* の商品を買い物かごに追加します。
9. **[!UICONTROL Checkout]** に移動し、プロンプトが表示されたら利用可能な *100* 報酬ポイントを使用して、注文します。
10. **[!UICONTROL Admin]**/**[!UICONTROL Sales]**/**[!UICONTROL Orders]**/**[!UICONTROL Invoice]** に移動し、その注文を出荷します。
11. [!UICONTROL Credit Memo] に移動し、*払い戻す数量* を *8* に更新します。
12. 「**[!UICONTROL Refund Reward Points]**」チェックボックスにチェックマークを入れて「**[!UICONTROL Refund offline]**」をクリックします。
13. [!UICONTROL Credit Memo] を使用して、注文から残りの 2 つの製品を返金してみてください。

<u> 期待される結果 </u>:

* 管理者は、残りの 2 つの製品を返す [!UICONTROL Credit Memo] を作成します。
* 注文のステータスは *完了* です。

<u> 実際の結果 </u>:

* これ以上 [!UICONTROL Credit Memo] を作成できません。
* 注文ステータスは *クローズ* です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
