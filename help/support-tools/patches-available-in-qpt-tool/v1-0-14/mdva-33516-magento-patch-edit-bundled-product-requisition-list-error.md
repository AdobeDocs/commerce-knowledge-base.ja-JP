---
title: 「MDVA-33516 パッチ：バンドルされた製品要求リストの編集エラー」
description: MDVA-33516 パッチは、要求リストからバンドル製品タイプを編集すると、要求リスト項目エラーページにリダイレクトされる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.14 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 76a16982-f977-4674-b05e-23f4ac355d52
feature: B2B, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# MDVA-33516 パッチ：バンドルされた製品要求リストの編集エラー

MDVA-33516 パッチは、要求リストからバンドル製品タイプを編集すると、要求リスト項目エラーページにリダイレクトされる問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.14 がインストールされています。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.4

**Adobe Commerce バージョンとの互換性：**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.0 - 2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

要求リストでバンドルされた製品を編集中にエラーが発生しました。

<u>前提条件</u>:

* B2B がインストールされています。
* 購買依頼リストが使用可能です。

<u>再現手順</u>:

1. 2 つのシンプルな製品でバンドルされた製品を作成します。
1. バンドルされた製品ページに移動し、 **カスタマイズしてカートに追加** ボタン。
1. ドロップダウンからオプションの 1 つを選択し、クリックします。 **購買依頼リストに追加** 新規購買依頼リストを作成する手順は、次のとおりです。 詳細な手順については、次を参照してください [Magento・ユーザー・ガイド > 「自分の購買依頼リスト」 > 「購買依頼リストの作成」](https://docs.magento.com/user-guide/customers/account-dashboard-requisition-lists.html#create-a-requisition-list) を参照してください。
1. 新しく作成した購買依頼リスト（「自分アカウント」）に移動します。 **マイ購買依頼リスト**）に設定します。
1. 「」をクリックします **表示** のボタン *アクション* 列。
1. 「」をクリックします **編集** ボタン。

<u>期待される結果</u>:<br>

エラーはありません。

<u>実際の結果</u>:

「カスタマイズ」ページ。バンドルされた製品の画像、価格、次のエラーメッセージが含まれます。

```
Fatal error: Uncaught Error: Call to a member function isAvailableForCompare() on null in /var/www/html/var/view_preprocessed/pub/static/vendor/magento/module-catalog/view/frontend/templates/product/view/addto/compare.phtml:1 Stack trace: #0 /var/www/html/vendor/magento/framework/View/TemplateEngine/Php.php(59): include() #1 /var/www/html/vendor/magento/framework/View/Element/Template.php(271): Magento\Framework\View\TemplateEngine\Php->render(Object(Magento\Catalog\Block\Product\View\AddTo\Compare), '/var/www/html/v...', Array) #2 /var/www/html/vendor/magento/framework/View/Element/Template.php(301): Magento\Framework\View\Element\Template->fetchView('/var/www/html/v...') #3 /var/www/html/vendor/magento/framework/View/Element/AbstractBlock.php(1099): Magento\Framework\View\Element\Template->_toHtml() #4 /var/www/html/vendor/magento/framework/View/Element/AbstractBlock.php(1103): Magento\Framework\View\Element\AbstractBlock->Magento\Framework\View\Element   {closure} () #5 /var/www/html/vendor/magento/framework/View/Element/ in /var/www/html/var/view_preprocessed/pub/static/vendor/magento/module-catalog/view/frontend/templates/product/view/addto/compare.phtml
  on line 1
```

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
