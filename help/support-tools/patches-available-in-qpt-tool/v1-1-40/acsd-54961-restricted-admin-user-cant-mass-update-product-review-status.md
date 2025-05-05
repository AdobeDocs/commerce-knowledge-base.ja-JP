---
title: 「ACSD-54961：制限付き管理者ユーザーは、[!UICONTROL Product Review status] を一括更新できない」
description: ACSD-54961 パッチを適用して、制限付き管理者ユーザーは製品レビューステータスを一括更新できないAdobe Commerceの問題を修正してください。
feature: Products
role: Admin, Developer
exl-id: 26c5bacd-21de-4533-a7b6-4acbacd38fec
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# ACSD-54961：制限付き管理者ユーザーは、[!UICONTROL Product Review status] を一括更新できません

ACSD-54961 パッチは、制限付き管理者ユーザーが [!UICONTROL Product Review status] ータを一括更新できない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされている場合に使用できます。 パッチ ID は ACSD-54961 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

制限付き管理者ユーザーは、[!UICONTROL Product Review status] を一括更新できません。

<u> 再現手順 </u>:

1. 追加の web サイト、ストア、ストア表示を作成します。
1. 商品を 2 番目のストアに追加し、レビューを追加します。
1. 2 つ目のストアへのアクセス権のみを持つ、制限付きの管理者ユーザーを作成します。
1. 制限付き管理者ユーザーとしてログインし、**[!UICONTROL &#x200B; Marketings]**/**[!UICONTROL Reviews]**/**[!UICONTROL Mass Update]** に移動して、**ステータス** を *承認済み* または *保留中* に設定します。

<u> 期待される結果 </u>:

制限付き管理者ユーザーは、**[!UICONTROL Mass Update]** アクションを使用してレビューを更新できます。

<u> 実際の結果 </u>:

アクションを使用してレビューを更新する際にエラー **[!UICONTROL Mass Update]** 発生します。<br>
`var/log/exception.log` に同様のエラーが含まれています。

```
report.CRITICAL: TypeError: array_intersect(): Argument #1 ($array) must be of type array, null given in app/code/Magento/AdminGws/Model/Models.php:439
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
