---
title: 「ACSD-54885：管理者が顧客としてログインした際、複数のアドレスのチェックアウト中に例外が発生する」
description: 管理者がを使用している際に、複数のアドレスのチェックアウト中にエラーが発生するAdobe Commerceの問題を修正するために、ACSD-54885 パッチを適用します。[!UICONTROL Login as Customer]*機能。
feature: Checkout
role: Admin, Developer
exl-id: 524ec96b-1465-4673-9fbe-1a9c086b7e87
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# ACSD-54885：管理者が顧客としてログインした際に、複数のアドレスのチェックアウト中に例外が発生する

ACSD-54885 パッチでは、管理者がを使用している際に、複数のアドレスのチェックアウト中にエラーが発生する問題を修正しています。 *[!UICONTROL Login as Customer]* 機能。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされています。 パッチ ID は ACSD-54885 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者がを使用しているときに、複数のアドレスのチェックアウト中にエラーが発生します *[!UICONTROL Login as Customer]* 機能。

<u>再現手順</u>:

1. を確実にする *[!UICONTROL Login as Customer]* が有効になっています。 に移動 **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Configurations]** > **[!UICONTROL Advanced]** > **[!UICONTROL Admin]** > **[!UICONTROL Admin Actions]** > **[!UICONTROL Logging]** > **[!UICONTROL Login as Customer]**.
1. シンプルな製品を作成します。
1. 住所を使用して新しい顧客アカウントを作成します。
1. バックエンドの顧客アカウントに移動します。

   * に移動します **[!UICONTROL Account Information]** タブ、設定 *[!UICONTROL Allow remote shopping assistance]* = *はい*.
   * クリック **[!UICONTROL Login as Customer]**.

1. 商品を買い物かごに追加し、次の手順に進みます *[!UICONTROL Checkout with multiple addresses]*.
1. 製品数量を更新します。
1. 買い物かごに戻ってみてください。

<u>期待される結果</u>:

買い物かごを更新し、複数の住所のチェックアウトを使用できます。

<u>実際の結果</u>:

買い物かごに戻ると、次のエラーが発生します。

```PHP
report.CRITICAL: Error: Call to a member function getCustomer() on null in magento2ee/app/code/Magento/LoginAsCustomerLogging/Observer/LogUpdateQtyObserver.php:88
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
