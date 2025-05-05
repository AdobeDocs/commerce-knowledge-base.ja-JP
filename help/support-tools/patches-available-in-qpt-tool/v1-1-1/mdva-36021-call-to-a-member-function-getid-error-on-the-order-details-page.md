---
title: 「MDVA-36021：注文の詳細を開くと、ユーザーにエラーメッセージが表示される」
description: MDVA-36021 パッチを適用すると、注文の詳細を開こうとしたときに、ユーザがメンバ関数 getId （）の呼び出しを受け取るというエラーメッセージが表示される問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.1 がインストールされている場合に利用できます。 パッチ ID は MDVA-36021。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 73b1f3c6-5dc4-48e4-8f3f-681be84f7638
feature: Orders
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# MDVA-36021：注文の詳細を開くとエラーメッセージが表示される

MDVA-36021 パッチは、注文の詳細を開こうとすると、ユーザが *メンバ関数 getId （）の呼び出し* というエラーメッセージを受け取る問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.1 がインストールされている場合に使用できます。 パッチ ID は MDVA-36021。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.4.1、2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーが注文の詳細を開こうとすると、管理の注文の詳細ページに次のエラーメッセージが表示されます。*report.CRITICAL: エラー：/magento2ce/app/code/Magento/Sales/view/adminhtml/templates/order/totals/tax.phtml:62* の配列でメンバー関数 getId （）を呼び出します。

<u> 前提条件 </u>:

システムには、特定の税率を持つ税金設定と注文が必要です。

<u> 再現手順 </u>:

1. Commerce Admin にログインします。
1. **売上**/**受注**/**受注をオープン** に移動します。

<u> 期待される結果 </u>:

注文はエラーなしで開かれます。

<u> 実際の結果 </u>:

次のようなエラーメッセージが表示されます。*report.CRITICAL: エラー：/magento2ce/app/code/Magento/Sales/view/adminhtml/templates/order/totals/tax.phtml:62* の配列のメンバー関数 getId （）の呼び出し。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
