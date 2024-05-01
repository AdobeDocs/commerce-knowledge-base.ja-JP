---
title: '''ACSD-54989：次の場合、会社管理者は注文できません [!UICONTROL Enable Purchase Orders] 「はい」に設定し、 [!UICONTROL Purchase Order] 「いいえ」に設定'
description: 次の場合に、会社管理者が注文できないAdobe Commerceの問題を修正するために ACSD-54989 パッチを適用してください [!UICONTROL Enable Purchase Orders] が「はい」に設定され、 [!UICONTROL Purchase Order] は「いいえ」に設定されています。
feature: Orders, Companies, Purchase Orders
role: Admin, Developer
exl-id: c2850409-d310-4681-80ec-af8ba347854c
source-git-commit: 35cd21581ee34a6213be42a79e159439b8856fb6
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# ACSD-54989：会社管理者は、次の場合に注文できません *[!UICONTROL Enable Purchase Orders]* をに設定 *はい* および *[!UICONTROL Purchase Order]* をに設定 *不可*

ACSD-54989 パッチは、次の場合に注文できない問題を修正します **[!UICONTROL Enable Purchase Orders]** をに設定 *はい* および **[!UICONTROL Purchase Order]** をに設定 *不可*. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされています。 パッチ ID は ACSD-54989 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p5 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

会社管理者は、次の場合に注文できません **[!UICONTROL Enable Purchase Orders]** はに設定されています。 *はい* および **注文書** をに設定 *不可*.

<u>前提条件</u>:

インストール [!DNL B2B] モジュール。

<u>再現手順</u>:

1. 会社と休暇を有効にする [!UICONTROL **Order Approval Configuration]** > **[!UICONTROL Purchase Order**] = *不可*.
1. 100 の価格で簡単な製品を作成してください。
1. 管理者を通じて会社を新規作成します。
1. を設定 [!UICONTROL **発注書を有効にする**] 対象： *はい*.
1. ストアフロントで会社管理者としてログインします。
1. 作成したシンプルな製品を買い物かごに追加します。
1. チェックアウトページに進み、 **[!UICONTROL Place Order]** をクリックして購入を完了します。

<u>期待される結果</u>:

注文は正常に行えます。

<u>実際の結果</u>:

この **[!UICONTROL My Account]** ページが開き、注文は行われません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
