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

MDVA-43601 パッチでは、`catalogrule_rule` または `catalogrule_product` の完全な再インデックスの後 `catalogrule_product_price` テーブルからトリガーが削除される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.13 がインストールされている場合に使用できます。 パッチ ID は MDVA-43601。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`catalogrule_rule` または `catalogrule_product``catalogrule_product_price` 完全に再インデックスすると、トリガーはテーブルから削除されます。

<u> 再現手順 </u>:

1. すべてのインデクサーを *スケジュールに従って更新* に設定します。
1. 次の SQL リクエストを実行して、テーブル `catalogrule_product_price` 対して作成されたトリガーを確認します。

   ```sql
   show triggers like '%catalogrule_%'\G
   ```

1. 次のコマンドを実行して、`catalogrule_rule` または `catalogrule_product` のインデックスを手動で再作成します。`bin/magento indexer:reindex catalogrule_rule`
1. テーブルのトリガーを再度確認 `catalogrule_product_price` ます。

<u> 期待される結果 </u>:

テーブル内 `catalogrule_product_price`トリガーは、完全に再インデックスされても保持されます。

<u> 実際の結果 </u>:

テーブルのトリガーが見つかり `catalogrule_product_price` せん。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
