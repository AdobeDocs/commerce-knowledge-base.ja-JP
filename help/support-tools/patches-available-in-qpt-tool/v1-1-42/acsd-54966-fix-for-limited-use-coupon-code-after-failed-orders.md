---
title: 「ACSD-54966：注文が失敗した後のクーポンコードの再利用に関する修正」
description: 以前に失敗した注文に続いて、プロモーションや買い物かごごとに制限されているクーポンコードの再利用を防ぐAdobe Commerceの問題を修正するために ACSD-54966 パッチを適用してください。
feature: Promotions/Events, Shopping Cart, Orders
role: Admin, Developer
exl-id: 931cfe7a-30a3-4a7d-ada5-4e2d7084f3e1
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# ACSD-54966：注文が失敗した後のクーポンコードの再利用を修正

ACSD-54966 パッチは、以前に失敗した注文の後、顧客ごとに制限されているクーポンコードの再利用を妨げる問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.42 がインストールされています。 パッチ ID は ACSD-54966 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クーポンコードは、お客様ごとの 1 回の使用に制限されており、以前の注文が失敗した後で再利用することはできません。

<u>再現手順</u>:

1. で買い物かごの価格ルールを設定する *[!UICONTROL Uses per Customer]* = *1*.
1. 割り当てられたクーポンコードを使用して購入を行います。
1. 管理パネルから注文をキャンセルするか、支払いに失敗して注文を実行します。
1. 次のコマンドを実行します。 `bin/magento queue:consumers:start sales.rule.update.coupon.usage`
1. 同じ顧客に同じクーポンコードを使用して、後続の注文を試みます。

<u>期待される結果</u>:

注文をキャンセルした後、または支払いエラーが発生した後、顧客は新しい購入のためにクーポンコードを正常に再利用できます。

<u>実際の結果</u>:

お客様はクーポンコードを再利用できません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
