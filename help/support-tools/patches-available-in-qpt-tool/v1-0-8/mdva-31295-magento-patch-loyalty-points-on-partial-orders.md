---
title: 「MDVA-31295：部分的な注文に対するロイヤルティポイント」
description: MDVA-31295 パッチは、部分的な注文が完了し、品目に課税が行われると、報酬ポイントが正しく計算されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.8 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 10e8a3a9-bfab-4256-b772-fd64e8885da3
feature: Orders
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# MDVA-31295：部分的な注文に対するロイヤルティポイント

MDVA-31295 パッチは、部分的な注文が完了し、品目に課税が行われると、報酬ポイントが正しく計算されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.8 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce オンプレミス 2.3.0

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文が完了（部分的に出荷）し、商品に税金が課せられている場合、報酬は顧客のアカウントには適用されません。 アイテムが課税されない場合、報酬は正常に顧客アカウントに追加されます。

<u> 再現手順 </u>:

1. 顧客としてストアフロントにログインします。
1. 2 つの製品を買い物かごに追加します。
1. チェックアウトに移動し、税金が含まれる配送先住所を設定して、注文します。
1. 管理画面で、最近注文した商品に移動します。
1. **請求書** をクリックし、いずれかの品目について **請求書の数量** を 0 に設定して、**数量の更新** をクリックします。 請求書を発行します。
1. 「出荷」をクリックし、未請求の品目の **出荷数量** を 0 に設定します。 「**出荷の発行**」をクリックします。
1. 注文をキャンセルをクリックします。 ステータスが「完了」に設定されます。
1. 管理者で、**顧客**/以前に行った顧客の購入を選択/**報酬ポイント**/**報酬ポイント履歴** に移動します。
1. 注文の獲得報酬ポイントを確認します。

<u> 期待される結果 </u>:

報酬ポイントは、部分的な注文が完了したときに課税注文に対して計算する必要があります。

<u> 実際の結果 </u>:

部分的な注文が完了した場合、課税注文に対する報酬ポイントは計算されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
