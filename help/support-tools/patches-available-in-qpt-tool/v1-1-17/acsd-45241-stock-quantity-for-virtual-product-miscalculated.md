---
title: 「ACSD-45241：仮想製品の在庫数の計算ミス」
description: ACSD-45241 パッチは、クレジットメモを作成した後に仮想製品の在庫数が誤って計算される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.17 がインストールされている場合に利用できます。 パッチ ID は ACSD-45241 です。 この問題はAdobe Commerce 2.4.4 で修正されました。
exl-id: 4be97da9-d399-419a-816e-cf65f15cc3be
feature: Orders, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# ACSD-45241：仮想製品の在庫数の計算ミス

ACSD-45241 パッチは、クレジットメモを作成した後に仮想製品の在庫数が誤って計算される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.17 がインストールされている場合に使用できます。 パッチ ID は ACSD-45241 です。 この問題はAdobe Commerce 2.4.4 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

仮想商品の在庫数が、クレジットメモの作成後に誤って計算されます。

<u> 再現手順 </u>:

1. Commerce Admin で、バーチャル製品を子製品として使用して設定可能な製品を作成します。
1. 手順 1 で作成した両方の製品が在庫にあることを確認します。
1. 手順 1 で作成したバーチャル製品の数量を 100 としてマークし、販売可能数量を 100 のままにします。
1. 商品を買い物かごに追加します。
1. 手順 1 で作成した仮想製品で注文します。
1. 注文ステータスは「保留中」のままにします。 支払いを処理する必要はありません。
1. `inventory_reservation``order_created` 作成されたレコード。 仮想製品数量は 100 で、販売可能数量は 99 です。
1. 注文を開き、**請求書**/**請求書を送信** に移動します。
1. `inventory_reservation``invoice_created` 作成されたレコード。 仮想製品数量は 99 になり、販売可能数量も 99 になります。
1. 「在庫に戻る **を選択せずにクレジットメモを作成** ます。

<u> 期待される結果 </u>:

`inventory_reservation` に新しいレコードは作成されず、バーチャル製品の在庫数は変更されません。

<u> 実際の結果 </u>:

`inventory_reservation` で `creditmemo_created` レコードが作成され、仮想製品の在庫数は 98 に調整され、販売可能数は 99 になります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
