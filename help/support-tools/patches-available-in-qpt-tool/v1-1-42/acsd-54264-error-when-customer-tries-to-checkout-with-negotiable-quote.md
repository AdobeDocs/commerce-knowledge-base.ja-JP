---
title: 「ACSD-54264：お客様が交渉可能な見積もりでチェックアウトしようとするとエラーが発生する」
description: Adobe Commerce ACSD-54264 パッチを適用すると、「リクエストされた属性を更新できません。 Row ID:store_id」は、顧客が別のストアビューから交渉可能な見積もりでチェックアウトしようとすると表示されます。
feature: B2B, Checkout
role: Admin, Developer
exl-id: de8f451e-3b0a-4721-9ff4-18553477db1d
source-git-commit: 2e344b1ca4bc075bdbc9074bb431a398f0871698
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# ACSD-54264：お客様が交渉可能な見積もりでチェックアウトしようとすると、エラーが表示される

ACSD-54264 パッチは、エラーメッセージが表示される問題を修正します *リクエストされた属性を更新することはできません。 行 ID: store_id* 顧客が別のストア表示から交渉可能な見積もりでチェックアウトを試みたときに表示されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.42 がインストールされています。 パッチ ID は ACSD-54264 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

エラーメッセージ *リクエストされた属性を更新することはできません。 行 ID: store_id* 顧客が別のストア表示から交渉可能な見積もりでチェックアウトを試みたときに表示されます。

<u>前提条件</u>:

Adobe Commerce B2B モジュールがインストールされ、有効になっています。

<u>再現手順</u>:

1. デフォルトの web サイト用に、追加のストア表示を作成します。
1. を有効にする *[!UICONTROL B2B Quote]* 設定で指定します。
1. ストア表示のいずれかで会社の顧客としてログインします。
1. に製品を追加する *[!UICONTROL Shopping Cart]*.
1. 見積をレビュー用に発行します。
1. 管理者ユーザーとして、に移動します。 **[!UICONTROL Sales]** > **[!UICONTROL Quotes]** 承認された見積もりを送信します。
1. 会社の顧客として、ストア表示を別のストア表示に変更します。
1. チェックアウトしてみてください。

<u>期待される結果</u>:

顧客はこの見積もりで注文を行います。

<u>実際の結果</u>:

* エラーは、配送情報の保存中に発生します。

  `You cannot update the request attribute. Row ID: store_id =#`

* 次のエラーがログに記録されます。

  `report.CRITICAL: Magento\Framework\Exception\InputException: You cannot update the requested attribute. Row ID: store_id = 2. in /app/code/Magento/NegotiableQuote/Plugin/Quote/Model/QuoteUpdateValidator.php:100`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
