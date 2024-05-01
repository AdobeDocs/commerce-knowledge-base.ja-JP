---
title: 「ACSD-49497：発送後の注文が引き続き処理され、一部返金が行われます」
description: ACSD-49497 パッチを適用すると、Adobe Commerceの問題が修正されます。この問題では、出荷後も注文ステータスが処理中のままになり、部分的な払い戻しが適用されます。
exl-id: d195bcf4-bb8b-4373-8aad-a5b953b07443
feature: Admin Workspace, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# ACSD-49497：出荷後の注文の処理と一部返金

ACSD-49497 パッチは、出荷後に注文ステータスが処理中のままになり、部分的な払い戻しが適用される問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされています。 パッチ ID は ACSD-49497 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 - 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

新しい注文のステータスは「」に残ります *[!UICONTROL Processing]* 出荷後も状態を示し、部分的な払い戻しが適用されます。

<u>再現手順</u>:

1. 複数の品目を持つオーダーを作成します。
1. 送信元 **[!UICONTROL Admin]**&#x200B;注文の請求書を作成します。
1. 送信元 **[!UICONTROL Admin]**&#x200B;クレジット・メモを作成し、品目の一部のみを払い戻します。
1. 送信元 **[!UICONTROL Admin]**、注文の残りの項目の出荷をリクエストします。
1. 注文ステータスを確認します。

<u>期待される結果</u>:

注文のステータスは次のようになります *[!UICONTROL Complete]*.

<u>実際の結果</u>:

注文のステータスは残ります *[!UICONTROL Processing]*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
