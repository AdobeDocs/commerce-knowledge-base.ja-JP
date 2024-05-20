---
title: 「ACSD-51036:REST API の同時呼び出し時の競合状態によって、出荷ステータスが上書きされる」
description: ACSD-51036 パッチを適用すると、同時に REST API が呼び出され、注文された商品テーブルの配送ステータスが上書きされる際に競合状態が発生するAdobe Commerceの問題を修正できます。
exl-id: 12d90de7-fe5c-4fcc-b84a-d420dcd871ca
feature: REST, Orders, Shipping/Delivery
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# ACSD-51036:REST API の同時呼び出し時の競合状態により、順序付き項目テーブルで出荷ステータスが上書きされます

ACSD-51036 パッチでは、REST API の同時呼び出し時の競合状態によって、順序付き項目テーブルの出荷ステータスが上書きされる問題が修正されています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.31 がインストールされています。 パッチ ID は ACSD-51036 です。 この問題はAdobe Commerce 2.4.5 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

REST API の同時呼び出し時の競合状態により、順序付き項目テーブルの出荷ステータスが上書きされます。

<u>再現手順</u>:

1. 2 つの項目で注文を作成します。
1. 請求書項目 A.
1. REST API を介して品目 A の払い戻しリクエストを同時に送信すると同時に、品目 B の出荷リクエストを送信します。
1. 注文に進む **[!UICONTROL Admin Panel]**.

<u>期待される結果</u>

*[!UICONTROL Shipped 1]* 項目 B のステータスが「」に表示されます。 *[!UICONTROL Items]* 順序付きテーブル。

<u>実際の結果</u>

*[!UICONTROL Shipped 1]* の項目 B にステータスがありません *[!UICONTROL Items]* 順序付きテーブル。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
