---
title: 「ACSD-45424：一部払い戻し後に作成された予約報酬が正しくありません」
description: ACSD-45424 パッチは、部分的な払い戻しの後に誤った予約報酬が作成される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.17 がインストールされている場合に利用できます。 パッチ ID は ACSD-45424 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 0676cfda-a28e-4a66-a75b-8a3fc5e22566
feature: Orders
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# ACSD-45424：一部払い戻し後に作成された予約報酬が正しくありません

ACSD-45424 パッチは、部分的な払い戻しの後に誤った予約報酬が作成される問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.17 がインストールされています。 パッチ ID は ACSD-45424 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

一部払い戻し後に、誤った予約報酬が作成されます。

<u>再現手順</u>:

1. 店舗内配送配送方法を有効にします。
1. 3 つの在庫ソースを作成し、それぞれに集荷場所がアクティブであることを確認します（source1、source2、source3）。
1. 新しい在庫を作成し、3 つのソースを新しい在庫に割り当てます。
   * この在庫は、メインの web サイトに割り当てる必要があります。
1. 単純な製品 P3 を作成し、すべてのソースを割り当てます。
1. 単純製品のソースに次の数量を追加し、バックオーダーを有効化します。
   * デフォルトソース - 100
   * ソース 1 - 0
   * ソース 2 - 10
   * ソース 3 - 0
1. フロントエンドからカートにシンプルな製品を追加し、配送フォームに進みます。
1. 出荷場所として「source1」を選択します。
1. 注文を完了し、データベースで次のクエリを実行します。

   ```sql
   SELECT * FROM inventory_reservation WHERE sku = 'P3';
   ```

   注文レコードは次の場所に配置されます。 `inventory_reservation` テーブル。 数量は 10 で、これは正しい値です。
1. この注文をバックエンドから請求します。
1. これで、1 つの製品のみのクレジットメモを作成します。 を選択しないでください *在庫に戻る* チェックボックス。
1. 手順 8 で同じクエリを実行します。

<u>期待される結果</u>:

を選択しなかった場合 *在庫に戻る* クレジット・メモの作成中、 `inventory_reservation` テーブルには、クレジット メモに対応するレコードはありません。

<u>実際の結果</u>:

を選択しなかった場合でも *在庫に戻る* クレジットメモの作成中に、レコードがに追加されます。 `inventory_reservation` 次を含むテーブル `creditmemo_created` イベントタイプ。 また、 `inventory_reservation` 1 つの数量に対してのみクレジット・メモを作成した場合でも、表の数量は 10 です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
