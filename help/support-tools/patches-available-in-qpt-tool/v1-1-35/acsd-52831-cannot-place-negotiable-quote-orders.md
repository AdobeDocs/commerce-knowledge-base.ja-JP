---
title: 'ACSD-52831：次の場合は、交渉可能な見積注文を行えません [!DNL Google reCAPTCHA v3 Invisible] 有効'
description: 次の場合に交渉可能な見積注文を行うことができないAdobe Commerceの問題を修正するために、ACSD-52831 パッチを適用してください [!DNL Google reCAPTCHA v3 Invisible] が有効になっています。
feature: Quotes, B2B, Checkout
role: Admin
exl-id: 80cf5592-0784-4b37-8373-abec0847a9f0
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# ACSD-52831：次の場合は交渉可能な見積注文を行えません [!DNL Google reCAPTCHA v3 Invisible] enabled

ACSD-52831 パッチは、次の場合に交渉可能な見積注文を行うことができない問題を修正します [!DNL Google reCAPTCHA v3 Invisible] が有効になっています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-52831 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

次の場合は交渉可能な見積注文を行えません [!DNL Google reCAPTCHA v3 Invisible] が有効になっています。

<u>再現手順</u>:

1. B2B の引用機能を有効にします。
1. Enable （有効） [!DNL Google reCAPTCHA v3 Invisible] ストアフロントで、チェックアウト/注文を有効にします。
1. 見積もりを上げ、その見積もりでチェックアウトに進みます。
1. CAPTCHA エラーが発生したため、注文することはできません。

<u>期待される結果</u>:

見積もりはチェックアウトに進みます。

<u>実際の結果</u>:

次のエラーが発生します *reCAPTCHA 検証に失敗しました。再試行してください*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
