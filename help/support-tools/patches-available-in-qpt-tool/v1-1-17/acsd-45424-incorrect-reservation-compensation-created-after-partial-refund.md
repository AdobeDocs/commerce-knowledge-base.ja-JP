---
title: 「ACSD-45424：一部払い戻し後に作成された予約報酬が正しくありません」
description: ACSD-45424 パッチは、部分的な払い戻しの後に誤った予約報酬が作成される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.17 がインストールされている場合に利用できます。 パッチ ID は ACSD-45424 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 0676cfda-a28e-4a66-a75b-8a3fc5e22566
feature: Orders
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# ACSD-45424：一部払い戻し後に作成された予約報酬が正しくありません

ACSD-45424 パッチは、部分的な払い戻しの後に誤った予約報酬が作成される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.17 がインストールされている場合に使用できます。 パッチ ID は ACSD-45424 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

一部払い戻し後に、誤った予約報酬が作成されます。

<u> 再現手順 </u>:

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

   注文したレコードは `inventory_reservation` のテーブルに表示されます。 数量は 10 で、これは正しい値です。
1. この注文をバックエンドから請求します。
1. これで、1 つの製品のみのクレジットメモを作成します。 「*在庫に戻る*」チェックボックスを選択しないでください。
1. 手順 8 で同じクエリを実行します。

<u> 期待される結果 </u>:

クレジット・メモの作成時に *Return to Stock* を選択しなかった場合、クレジット・メモに対応するレコードは `inventory_reservation` の表には含まれません。

<u> 実際の結果 </u>:

クレジットメモの作成時に *Return to Stock* を選択しなくても、イベントタイプを使用してテーブルにレコード `inventory_reservation` 追加 `creditmemo_created` れます。 また、`inventory_reservation` 表に追加されたクレジット・メモ・レコードの数量は 10 ですが、クレジット・メモを作成した数量は 1 つのみです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
