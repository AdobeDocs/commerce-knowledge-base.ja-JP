---
title: 非表示 [!DNL reCAPTCHA] チェックアウト中に失敗し、注文を送信できない
description: が非表示になるAdobe Commerceの問題を修正するには、ACSD-54656 パッチを適用します [!DNL reCAPTCHA] がチェックアウト時に正しく機能しないので、注文の配置が妨げられます。
feature: Checkout, Gift
role: Admin, Developer
exl-id: dc26659e-ca34-461e-af91-b230c5afa919
source-git-commit: fe6269ac042326a85a2cab5ccf834ac3eff1c166
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# ACSD-54656：非表示 [!DNL reCAPTCHA] がチェックアウト時に正しく機能しないので、注文の配置が妨げられます。

ACSD-54656 パッチは、が非表示になる問題を修正します [!DNL reCAPTCHA] がチェックアウト時に正しく機能しないので、注文の配置が妨げられます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.46 がインストールされています。 パッチ ID は ACSD-54656 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

非表示 [!DNL reCAPTCHA] がチェックアウト時に正しく機能しないので、注文の配置が妨げられます。

<u>再現手順</u>:

1. あらゆるタイプの [!DNL reCAPTCHA] ギフトカード用 [!UICONTROL Checkout] ページ。
1. 買い物かごに製品を追加して、に移動する **[!UICONTROL Checkout]** ページ。
1. ギフトカードフォームを展開し、有効なギフトカードクーポンを入力します。
1. クリックする **[!UICONTROL See balance and apply]** ボタン。

<u>期待される結果</u>:

ギフト カードが正常に適用されました。

<u>実際の結果</u>:

エラーメッセージが表示されます。 *[!DNL reCAPTCHA]検証に失敗しました。再試行してください。*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
