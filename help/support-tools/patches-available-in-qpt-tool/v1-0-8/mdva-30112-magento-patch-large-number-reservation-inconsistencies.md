---
title: 'MDVA-30112：大量の予約の不整合'
description: MDVA-30112 パッチは、「inventory_reservation」テーブルに予期せず多数の [reservation inconsistencies] （https://devdocs.magento.com/guides/v2.4/inventory/inventory-cli-reference.html#what-causes-reservation-inconsistencies）がある問題を解決します。 予約の不整合には、未登録の未登録オープン注文と未登録の完了注文が含まれます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.8 がインストールされている場合に利用できます。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。
exl-id: db74fb61-dfeb-4e99-8513-d36fd68d2267
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# MDVA-30112：大量の予約の不整合

MDVA-30112 パッチを適用すると、`inventory_reservation` テーブルに予期せず多数の [ 予約の不整合 ](https://devdocs.magento.com/guides/v2.4/inventory/inventory-cli-reference.html#what-causes-reservation-inconsistencies) が存在する問題が解決されます。 予約の不整合には、未登録の未登録オープン注文と未登録の完了注文が含まれます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.8 がインストールされている場合に使用できます。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー 2.3.5 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.4 - 2.3.5-p2、2.4.0 - 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[bunch-size](https://devdocs.magento.com/guides/v2.4/inventory/inventory-cli-reference.html#list-inconsistencies-command) 値は、一度に読み込む注文の数の値です。 この値より多くの注文がある場合、Adobe Commerceは保留中ステータスの注文を不整合と見なします。

>[!NOTE]
>
>他の 3 つのインベントリ不整合の問題を修正するパッチ MDVA-33281 があります。 これには、CLI で `bin/magento inventory:reservation:list-inconsistencies` を実行しているときに発生する PHP Fatal エラーが含まれます。 修正されているもう 1 つの問題は、不整合リストのデータが重複していることです。 また、注文前に予約が作成される問題（注文後の予約に基づく以前の認識）。 このソリューションについては、サポート情報ベースの [MDVA-33281: inventory inconsistency issues](/help/support-tools/patches-available-in-qpt-tool/v1-0-14/mdva-33281-magento-patch-inventory-inconsistency-issues.md) を参照してください。

<u> 前提条件 </u>:

CLI で次のコマンドを実行して、`inventory_reservation` テーブル内の予約の不整合を一覧表示します。

```
magento inventory:reservation:list-inconsistencies
```

予期せず多数の予約の不整合が発生する、またはコマンドが完了しない。

<u> 再現手順 </u>:

1. CLI で次のコマンドを実行して不整合を解決します。

   ```
   bin/magento inventory:reservation:list-inconsistencies -r | bin/magento inventory:reservation:create-compensations
   ```

1. 次の 3 つの注文を行います。
   * それぞれに 1 つの製品を割り当てます。
   * Check/Money Order の支払い方法を使用して、注文ステータスが「保留中」になるようにします。
1. 数量–1 の 3 つのレコードが `inventory_reservation` テーブルに表示されます。 CLI で次のコマンドを実行して、不整合を確認します。

   ```
   bin/magento inventory:reservation:list-inconsistencies
   ```

   この場合は、正しい結果は返されません。

1. CLI で次のコマンドを実行します。

   ```
   Execute bin/magento inventory:reservation:list-inconsistencies      --bunch-size 1
   ```

   「保留中」ステータス注文が不整合として表示されていることがわかります。

1. CLI で次のコマンドを実行します。

   ```
   bin/magento inventory:reservation:list-inconsistencies      -r --bunch-size 1 | bin/magento inventory:reservation:create-compensations
   ```

<u> 期待される結果 </u>:

Adobe Commerceは、「保留中」ステータスの注文の不整合を解決しないでください。 在庫の不整合は、「完了」、「クローズ」、「キャンセル」ステータスの注文で解決する必要があります。

<u> 実際の結果 </u>:

指定された束サイズの値を超える注文がある場合、Adobe Commerceは「保留中」ステータスの注文を不整合と見なし、同じ注文に対して複数の不整合の解決記録を追加します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
