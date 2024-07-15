---
title: 「ACSD-45781：ストアフロント検索フィールドがモバイルに表示されない」
description: MDVA-45781 パッチを適用すると、ストア フロント検索フィールドがモバイルに表示されない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-45781。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 0ae90f6d-1c04-4599-b21d-4d02fd6b36db
feature: Cache, Native Luma Frontend Development, Search
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# ACSD-45781：ストアのフロント検索フィールドがモバイルに表示されない

MDVA-45781 パッチを適用すると、ストア フロント検索フィールドがモバイルに表示されない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.19 がインストールされている場合に使用できます。 パッチ ID は MDVA-45781。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアフロント検索フィールドがモバイルに表示されない

<u> 再現手順 </u>:

1. Commerce管理者/**ストア**/**設定**/**カタログ**/**カタログ検索** に移動して、次のように設定します。
   * 検索Recommendationsを有効にして *いいえ*
   * 検索候補を有効にして *いいえ*
1. 「**設定を保存**」ボタンをクリックします。
1. キャッシュをクリーンアップします。
1. 標準の Luma テーマを使用して、モバイルで参照します。
1. 「**検索** ボタンをクリックします。

<u> 期待される結果 </u>:

入力検索フォームが表示されます。

<u> 実際の結果 </u>:

何も起こらない。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
