---
title: 「ACSD-50345：チェックアウト中の reCAPTCHA の問題」
description: ACSD-50345 パッチを適用すると、注文処理中およびチェックアウト中に reCAPTCHA v2 と v3 の検証が失敗するAdobe Commerceの問題を修正できます。
exl-id: ac8c8130-0e4d-4610-9a55-afa779cce7a0
feature: Checkout, Orders
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# ACSD-50345：チェックアウト中の reCAPTCHA の問題

ACSD-50345 パッチは、注文処理中およびチェックアウト中に reCAPTCHA v2 と v3 の検証が失敗する問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.31 がインストールされています。 パッチ ID は ACSD-50345 です。 この問題はAdobe Commerce 2.4.6 で部分的に修正され、Adobe Commerce 2.4.7 で完全に修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.5-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

**事例#1**

Google reCAPTCHA v2 が、支払いに失敗した後、リロードされない。

<u>再現手順</u>

1. 設定 **[!UICONTROL Google reCAPTCHA v2]** （*私はロボットではありません*）に設定します。
1. を有効にする **[!UICONTROL reCAPTCHA]** チェックアウト用。
1. をクリックせずに注文してみてください **[!UICONTROL reCAPTCHA]**.
1. ユーザーが、欠落している reCAPTCHA （*reCAPTCHA 検証に失敗しました。再試行してください*）、をクリックします。 **[!UICONTROL reCAPTCHA]** その後、注文してみてください。

<u>期待される結果</u>

間違った reCAPTCHA で注文されることはありません。

<u>実際の結果</u>

エラーが発生しました –  *reCAPTCHA 検証に失敗しました。再試行してください* および *ID = 4 のカートがありません*

**事例#2**

Google reCAPTCHA v3 Invisible がチェックアウト時に機能せず、注文できません。 `PlaceOrder` イベントがトリガーされない。

<u>再現手順</u>

1. の設定 **[!UICONTROL reCAPTCHA v3 Invisible]** から **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL Security]**.
1. Enable （有効） **[!UICONTROL reCAPTCHA v3 Invisible]** の下でのチェックアウト/注文 **[!UICONTROL Storefront]** タブ。
1. を使用して注文してみてください [!UICONTROL Check/Money order] 支払い方法。

<u>期待される結果</u>

注文は、 **[!UICONTROL reCAPTCHA]** オン。

<u>実際の結果</u>

をクリックした後 **[!UICONTROL Place Order]** ボタンをクリックすると無効になり、それ以上何も起こりません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
