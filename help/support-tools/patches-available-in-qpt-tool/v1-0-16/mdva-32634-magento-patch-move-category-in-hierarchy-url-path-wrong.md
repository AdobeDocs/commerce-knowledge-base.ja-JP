---
title: 「MDVA-32634 パッチ：階層 url_path 内のカテゴリの移動が正しくありません」
description: MDVA-32634 パッチを適用すると、階層内のカテゴリを移動した後にカタログカテゴリの url\_path が変更されない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.16 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: a445dea6-3834-479b-9044-b6d2b863a0b5
feature: Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# MDVA-32634 パッチ：階層 url_path のカテゴリの移動が正しくありません

MDVA-32634 パッチを適用すると、階層内のカテゴリを移動した後にカタログカテゴリの url\_path が変更されない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.16 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.1 - 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

階層内でカタログカテゴリを移動すると、誤った URL\_path が返される。 デフォルトのストア範囲\[ **id:0** \] に割り当てられたカテゴリの url\_path は、階層内でカテゴリを移動した後も変更されません。

<u> 再現手順 </u>:

1. Commerce Admin にログインします。 ルート カテゴリの下に次のカテゴリ構造を作成します：move-cat sub-move-cat sub-move-cat2 new-cat-move
1. 次のクエリを使用して、\[ catalog\_category\_entity\_varchar \] テーブルの値の割り当てのカテゴリ \[ url\_path \] 属性\[ id: 120 \] を確認します。

   ```sql
   SELECT * FROM catalog_category_entity_varchar WHERE attribute_id = 120 ORDER BY value_id DESC LIMIT 4;
   ```

   次のような結果が得られます。

   ```sql
   MariaDB [m24dev]> SELECT * FROM catalog_category_entity_varchar WHERE attribute_id = 120 ORDER BY value_id DESC LIMIT 4;
   ```

   \[ url\_path \] 値が生成され、すべてのストア スコープ \[ 0 \] に割り当てられました。 これは、B2B のないインスタンスと比較すると正しいです。
1. バックエンド カテゴリ リストに移動し、\[ move-cat \] をドラッグして\[ new-cat-move \] にドロップします。 これで、カテゴリは new-cat-move-cat sub-move-cat sub-move-cat2 のようになります。
1. 次のクエリを使用して、\[ catalog\_category\_entity\_varchar \] テーブルを確認します。

   ```sql
   SELECT * FROM catalog_category_entity_varchar WHERE attribute_id = 120 ORDER BY value_id DESC LIMIT 16;
   ```

<u> 期待される結果 </u>:

すべてのストア スコープ \[ 0 \] に割り当てられた url\_path も、新しいパスで更新する必要があります。

<u> 実際の結果 </u>:

すべてのストア スコープ \[ 0 \] に割り当てられた url\_path は、移動後にそのようなパスが存在しなくても変更されません。 また、各ストアに対して新しい url\_path 値が作成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
