---
title: 「MDVA-42410：クーポンレポートにはデフォルトの基本通貨のみが表示される」
description: MDVA-42410 パッチは、クーポンレポートに基本通貨のみが表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-42410。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: b442a2ce-1bd4-4f09-95fd-2c626e32f509
feature: Orders
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# MDVA-42410: クーポン レポートには既定の基本通貨のみが表示されます

MDVA-42410 パッチは、クーポンレポートに基本通貨のみが表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.12 がインストールされている場合に使用できます。 パッチ ID は MDVA-42410。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クーポンレポートには、デフォルトの基本通貨のみが表示されます。

<u> 再現手順 </u>:

1. 追加の web サイト、ストア、ストア表示を作成します。
1. この新しい Web サイトに別の通貨を設定します。 例えば、ユーロです。
1. **ストア**/**通貨レート** に移動し、通貨レートを **ユーロ** に設定します。
1. 特定のクーポンを使用して **買い物かご価格ルール** を作成します – **テスト**。
1. フロントエンドに移動し、新しい web サイトの **Test** クーポンを注文します。
1. **Reports**/**Sales**/**Coupons** に移動します。
1. 範囲ドロップダウンで新しい web サイトを選択します。
1. 統計を更新し、レポートを実行します。

<u> 期待される結果 </u>:

クーポンレポートでは、新しい web サイトの通貨がユーロとして表示されます。

<u> 実際の結果 </u>:

新しい web サイトのクーポンレポートでは、デフォルトの基本通貨（この場合は USD）が使用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
