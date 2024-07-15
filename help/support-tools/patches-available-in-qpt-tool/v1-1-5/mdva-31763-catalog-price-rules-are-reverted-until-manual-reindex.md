---
title: 「MDVA-31763：カタログ価格ルールは、手動で再インデックスするまで元に戻されます」
description: MDVA-31763 パッチは、カタログ価格ルールが手動で再インデックスされるまで元に戻される問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-31763。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: eb2dfd1a-6d12-4676-82c1-bf92c6fa9fda
feature: Catalog Management, Orders, Price Rules
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# MDVA-31763: カタログ価格ルールは、手動で再インデックスするまで元に戻されます

MDVA-31763 パッチは、カタログ価格ルールが手動で再インデックスされるまで元に戻される問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.5 がインストールされている場合に使用できます。 パッチ ID は MDVA-31763。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な製品 `catalogrule_product` 対して部分インデクサーを実行すると、カタログルールが表示されなくなります。

<u> 再現手順 </u>:

1. 管理バックエンドにログインします。
1. **ストア**/**属性**/**製品** に移動し、「manufacturer」属性を検索します。
   * いくつかのオプションを追加し、「プロモルール条件に使用」を *はい* に設定します。
1. **ストア**/**属性**/**属性セット** に移動します。
   * デフォルトの属性セットを選択し、そのセットに「manufacturer」属性を追加します。
1. いくつかのバリエーションを持つ設定可能な製品を作成します。
1. 以前に作成した設定可能な製品の「製造元」属性値を設定します。
1. カタログルールを作成：
   * アクティブ =はい
   * Web サイト = メイン Web サイト
   * 顧客グループ =未ログイン
   * 条件：製造元= \&lt; 設定可能な製品に対して選択された値 >
   * アクション：任意の割引
1. 完全なインデックスを作成します。
1. PDP の製品価格を確認し、価格が正しいことを確認してください。
1. 作成した設定可能な商品の「重み」属性を更新します。
1. PDP の製品価格を確認します。

<u> 期待される結果 </u>:

設定可能な製品に設定されたカタログ価格ルールは、部分再インデックス中に削除されません。

<u> 実際の結果 </u>:

設定可能な製品に設定されたカタログ価格ルールは、部分再インデックス中に表示されなくなります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
