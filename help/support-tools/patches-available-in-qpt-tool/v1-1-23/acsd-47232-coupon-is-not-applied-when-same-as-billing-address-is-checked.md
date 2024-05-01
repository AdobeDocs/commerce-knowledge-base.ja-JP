---
title: 'ACSD-47232：次の場合、クーポンは適用されません [!UICONTROL Same as Billing Address] チェック'
description: 次の場合にクーポンが適用されないAdobe Commerceの問題を修正するには、ACSD-47232 パッチを適用してください [!UICONTROL Same as Billing Address] がチェックされます。
exl-id: 29b95a0b-8792-4830-a1e5-ce977f8453ec
feature: Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# ACSD-47232：次の場合、クーポンは適用されません [!UICONTROL Same as Billing Address] チェック済み

ACSD-47232 パッチは、次の場合にクーポンが適用されない問題を修正します **[!UICONTROL Same as Billing Address]** がチェックされます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.23 がインストールされています。 パッチ ID は ACSD-47232 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

次の場合、クーポンは適用されません： **[!UICONTROL Same as Billing Address]** がチェックされます。

<u>再現手順</u>:

1. Adobe Commerceをインストールします。
1. 重み=を使用してシンプルな製品を作成 *8*.
1. デフォルトの請求先と配送先住所で新しい顧客を作成します。
1. クーポンを使用して買い物かご価格ルールを作成します。
   * 対象： **[!UICONTROL Conditions]** セクション、追加 *合計ウェイトが 5 以上*
1. で新しい注文を作成してみてください [!UICONTROL Commerce] 管理者。
   * 作成したばかりの顧客を使用します
   * 製品を追加
   * クーポンを適用してみてください

<u>期待される結果</u>:

クーポンが適用されます。

<u>実際の結果</u>:

次のようなエラーが表示されます。 *123 クーポンコードが無効です。 コードを確認して、もう一度試してください。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
