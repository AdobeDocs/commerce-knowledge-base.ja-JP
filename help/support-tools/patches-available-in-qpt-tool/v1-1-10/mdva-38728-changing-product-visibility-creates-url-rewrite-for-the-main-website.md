---
title: 「MDVA-38728：製品の表示を変更すると、メイン web サイトの URL が書き換えられる」
description: MDVA-38728 パッチを使用すると、2 番目の Web サイトの製品の表示を変更すると、メインの Web サイトの URL が書き換えられる問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.10 がインストールされている場合に利用できます。 パッチ ID は MDVA-38728。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: ad1d5f82-294d-485d-acd3-28c3cd0fbf56
feature: Products
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# MDVA-38728：製品の表示を変更すると、メイン Web サイトの URL が書き換えられます

MDVA-38728 パッチを使用すると、2 番目の Web サイトの製品の表示を変更すると、メインの Web サイトの URL が書き換えられる問題が解決されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.10 がインストールされています。 パッチ ID は MDVA-38728。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

2 番目の web サイトの製品の表示を変更すると、メインの web サイトの URL が書き換えられます。

<u>再現手順</u>:

1. 追加の Web サイト、ストア、ストアレビューを作成します。
1. シンプルな製品を作成します。
1. 表示をに設定 **個別に表示されない**.
1. 2 番目の web サイトにのみ製品を割り当てます。
1. その他すべての必須フィールドに入力します。
1. 商品を保存します。
1. MySQL キューを開始します。

   ```mysql
   bin/magento queue:consumers:start product_action_attribute.update &
   bin/magento queue:consumers:start product_action_attribute.website.update &
   ```

1. 製品リストに移動します。
1. 作成した製品を選択し、カタログと検索への一括更新を使用して表示属性を更新します。
1. URL の書き換えを確認します。

<u>期待される結果</u>:

書き換えは、製品が割り当てられている 2 番目の web サイトに対して作成されます。

<u>実際の結果</u>:

メイン web サイトに対して書き換えが作成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
