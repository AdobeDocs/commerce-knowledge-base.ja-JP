---
title: 「MDVA-30265：メール内のトラッキングリンクで 404 ページが返される」
description: MDVA-30265 パッチを使用すると、お客様が注文確認メールの出荷トラッキングリンクをクリックしたときに「404 Page not Found」エラーが発生する問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.5 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 53e1ca98-dfa0-445b-a71a-56fd01b630ec
feature: Communications
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# MDVA-30265：電子メール内のトラッキングリンクで 404 ページが返される

MDVA-30265 パッチを使用すると、お客様が注文確認メールの出荷トラッキングリンクをクリックしたときに「404 Page not Found」エラーが発生する問題を解決できます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.5 がインストールされています。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3 から 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文に対して出荷が作成されると、トラッキング情報と注文を追跡するためのリンクが記載されたメールが顧客に送信されます。 ただし、顧客がメール内の出荷トラッキングリンクをクリックすると、「404 ページが見つかりません」というエラーが返されます。

<u>再現手順</u>:

1. Adobe Commerce 2.4 のインストール手順については、次を参照してください [Composer を使用したAdobe Commerceのインストール](https://devdocs.magento.com/guides/v2.4/install-gde/composer.html) 開発者向けドキュメントを参照してください。
1. 注文します。
1. 管理パネルに移動します。 **売上** > **注文件数**. 作成した注文を探して開きます。
1. 出荷を作成し、追跡番号を追加します（運送業者= カスタム値）。 手順については、次を参照してください [受注管理 > 出荷の作成](https://docs.magento.com/user-guide/sales/shipments-create.html) を参照してください。
1. メールが届きます。 トラッキングリンクが機能しているかどうかを確認するには、トラッキングリンクをクリックします。
1. 請求書を作成します。 手順については、次を参照してください [Order Management > 「請求書の作成」](https://docs.magento.com/user-guide/sales/invoice-create.html) を参照してください。 次に、上記のトラッキングリンクをもう一度クリックします。

<u>期待される結果</u>:

トラッキングリンクは、請求書を作成した後でも機能するはずです。

<u>実際の結果</u>:

請求書を作成した後、トラッキングリンクが機能せず、「404 Page not Found」エラーページを返します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
