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

ACSD-55352 パッチでは、顧客報酬ポイントを含む部分的なクレジットメモを作成した後に注文ステータスが「」に変わる問題が修正されています *クローズ* また、クレジットメモオプションが管理注文ページに表示されなくなります。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.44 がインストールされています。 パッチ ID は ACSD-55352 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

顧客報酬ポイントを含む部分的なクレジットメモを作成した後、注文ステータスが「」に変わります *クローズ* また、クレジットメモオプションが管理注文ページに表示されなくなります。

<u>再現手順</u>:

1. Adobe Commerce Admin にログインします。
2. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Other Setting]** > **[!UICONTROL Reward Exchange Rates]** > **[!UICONTROL Add New Rate]**.
3. 2 つの料率を追加します。
   * *[!UICONTROL First]*:
      * *[!UICONTROL Direction]* = *ポイント先の通貨*
      * *[!UICONTROL Rate]* = *100*
      * *[!UICONTROL Upper Boundary]* = *100*
   * *[!UICONTROL Second]*:
      * *[!UICONTROL Direction]* = *通貨からポイント*
      * *[!UICONTROL Rate]* = *100*
      * *[!UICONTROL Upper Boundary]* = *100*
4. ～という値段で簡単な商品を作る *100 ドル* と *数量* : *100*.
5. ストアフロントから顧客を作成します。
6. もう一度バックエンドに移動します。 **[!UICONTROL Customers]** > **[!UICONTROL All Customers]** > **[!UICONTROL Edit]** > **[!UICONTROL Reward Points]** > **[!UICONTROL Update Points]** /追加 *100* そして、顧客を保存します。
7. ストアフロントに移動し、以前に作成した顧客としてログインします。
8. を使用した買い物かごへの製品の追加 *数量* : *10*.
9. に移動 **[!UICONTROL Checkout]** 使用可能なを使用します *100* プロンプトが表示されたらポイントを獲得して、注文します。
10. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Sales]** > **[!UICONTROL Orders]** > **[!UICONTROL Invoice]** その注文を出荷します。
11. に移動 [!UICONTROL Credit Memo] を更新します *払戻数量* 対象： *8*.
12. をティックします。 **[!UICONTROL Refund Reward Points]** チェックボックスをオンにして、 **[!UICONTROL Refund offline]**.
13. を使用して、注文から残りの 2 つの製品を返金してみてください [!UICONTROL Credit Memo].

<u>期待される結果</u>:

* 管理者が作成 [!UICONTROL Credit Memo] 残りの 2 つの製品を返します。
* 注文のステータスは *完了済み*.

<u>実際の結果</u>:

* これ以上作成できません [!UICONTROL Credit Memo].
* 注文のステータスは *クローズ*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
