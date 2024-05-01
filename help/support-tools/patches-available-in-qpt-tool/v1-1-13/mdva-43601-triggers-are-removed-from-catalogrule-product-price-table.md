---
title: 「MDVA-43601：完全な再インデックス後に、「catalogrule_product_price」テーブルからトリガーが削除される」
description: MDVA-43601 パッチは、「catalogrule_rule」または「catalogrule_product」の完全な再インデックスの後に「catalogrule_product_price」テーブルからトリガーが削除される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.13 がインストールされている場合に利用できます。 パッチ ID は MDVA-43601。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: fdef1e56-79ec-455a-8a29-b82f1c8ceea7
feature: Catalog Management, Orders, Products
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# MDVA-43601：完全な再インデックス後に、「catalogrule_product_price」テーブルからトリガーが削除される

MDVA-43601 パッチを適用すると、からトリガーが削除される問題が修正されます `catalogrule_product_price` の完全な再インデックス後のテーブル `catalogrule_rule` または `catalogrule_product`. このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.13 がインストールされています。 パッチ ID は MDVA-43601。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

トリガーがから削除されました `catalogrule_product_price` の完全な再インデックス後のテーブル `catalogrule_rule` または `catalogrule_product`.

<u>再現手順</u>:

1. すべてのインデクサーをに設定 *スケジュールで更新*.
1. で作成されたトリガーを確認します `catalogrule_product_price` 次の SQL リクエストを実行してテーブルに追加します。

   ```sql
   show triggers like '%catalogrule_%'\G
   ```

1. 手動での再インデックス化 `catalogrule_rule` または `catalogrule_product` 次のコマンドを実行します。 `bin/magento indexer:reindex catalogrule_rule`
1. トリガーを確認する `catalogrule_product_price` もう一度表に出なさい。

<u>期待される結果</u>:

のトリガー `catalogrule_product_price` 完全な再インデックスの後、テーブルは保持されます。

<u>実際の結果</u>:

のトリガーが見つかりません `catalogrule_product_price` テーブル。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
