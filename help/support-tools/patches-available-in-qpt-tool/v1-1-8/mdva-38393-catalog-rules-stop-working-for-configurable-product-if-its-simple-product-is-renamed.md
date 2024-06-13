---
title: 「MDVA-38393：シンプルな製品の名前が変更されると、設定可能な製品のカタログルールが機能しなくなる」
description: MDVA-38393 パッチは、設定可能な製品の単純な製品の名前が変更されると、その製品のカタログルールが機能しなくなる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.8 がインストールされている場合に利用できます。 パッチ ID は MDVA-38393。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: a20856c4-8aff-427b-a404-7afe706be06f
feature: Catalog Management, Categories, Configuration, Products
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# MDVA-38393：設定可能な製品の単純な製品の名前が変更されると、その製品のカタログルールは機能しなくなります

MDVA-38393 パッチは、設定可能な製品の単純な製品の名前が変更されると、その製品のカタログルールが機能しなくなる問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.8 がインストールされています。 パッチ ID は MDVA-38393。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な製品の単純な製品の名前が変更されると、カタログルールはその製品の機能を停止します。

<u>再現手順</u>:

1. 関連付けられたシンプルなプロダクトを使用して、設定可能なプロダクトを作成します。
1. カテゴリを作成します。
1. 設定可能な製品のみを新しいカテゴリに割り当てます。
1. 新しいカタログルールを作成します。
   * 条件= カテゴリに\が含まれている&lt;new category=&quot;&quot; id=&quot;&quot;>
   * アクション = 50% 割引
   * アクティブ =はい
1. 再インデックスを実行します。
1. フロントエンドで設定可能な製品を確認します（割引を適用する必要があります）。
1. を確認します `catalogrule_product` テーブル （シンプルな商品には割引が必要です）。
1. 管理者に移動して、シンプルな製品の名前を変更します。 これにより、 `catalogrule_product_cl` テーブル。
1. Cron または `bin/magento cron:run --group=index --bootstrap=standaloneProcessStarted=1` コマンド。
1. を確認します `catalogrule_product` テーブル。

<u>期待される結果</u>:

設定可能な製品には割引があります。

<u>実際の結果</u>:

* シンプルな商品に対して作成された割引レコードが `catalogrule_product` テーブル。
* フロントエンドの設定可能な製品は、完全なオリジナルの価格を持っています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
