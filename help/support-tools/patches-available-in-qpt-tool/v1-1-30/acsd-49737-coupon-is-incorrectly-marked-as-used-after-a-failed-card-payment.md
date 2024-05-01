---
title: 「ACSD-49737：カードの支払いに失敗した後、クーポンが誤って使用済みとしてマークされる」
description: ACSD-49737 パッチを適用すると、カード支払いが失敗した後にクーポンが誤って使用済みとしてマークされるAdobe Commerceの問題を修正できます。
exl-id: 77b5ec9c-3c4c-4da3-ba7e-8be3ccea04d0
feature: Orders, Payments
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# ACSD-49737：クーポンが正しく次のようにマークされていません *使用済み* カードの支払いが失敗した後

ACSD-49737 パッチは、クーポンが正しくとしてマークされていない問題を修正します *使用済み* カードの支払いが失敗した後。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は ACSD-49737 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1-p1 - 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クーポンが正しく次のようにマークされていません： *使用済み* カードの支払いが失敗した後。

<u>前提条件</u>:

1. の設定 **[!UICONTROL Braintree sandbox payment]** メソッド。
1. 必ずを実行してください [*sales.rule.update.coupon.usage*](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/consumers.html?lang=en) コンシューマーが設定および実行されています。

<u>再現手順</u>:

1. を作成 **[!UICONTROL Cart Price Rule]** 自動生成されたクーポンコードを使用。
1. 顧客としてログインします。
1. 商品を買い物かごに追加します。
1. 自動生成されたクーポンコードを適用します。
1. 失敗した支払いで注文してみてください。
1. でのクーポンの使用状況の確認 **[!UICONTROL Cart Price Rule]** の下 **[!UICONTROL Manage Coupon Codes]** タブ。

<u>期待される結果</u>:

クーポンに次のフラグを設定しないでください *使用済み* 支払いが失敗した場合。

<u>実際の結果</u>:

* クーポンコードに次のように表示 – 使用済み： *はい*、回使用： *1*
* クーポンコードは 1 回限りの使用にのみ有効です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## パッチのインストール後に必要な追加手順

（この節はオプションです。問題を修正するためにパッチを適用した後に必要な手順が含まれる場合があります）。 

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
