---
title: 「MDVA-34591：買い物かご価格ルールの計算が期待どおりに行われない」
description: 複数の買い物かご価格ルールが適用されている場合、**最大数量割引が適用される**買い物かご価格ルールが正しく機能しない問題が、MDVA-34591 パッチで修正されました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-34591。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。
exl-id: 1fa196bb-aab1-4364-a1b0-7c31d6d27d6d
feature: Orders, Price Rules, Shopping Cart
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# MDVA-34591：買い物かごの価格ルールの計算が期待どおりに行われない

MDVA-34591 パッチは、買い物かごの価格ルールに **最大数量割引の適用対象** 複数の買い物かご価格ルールが適用されている場合、は正しく機能しません。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.19 がインストールされています。 パッチ ID は MDVA-34591。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.6

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0-2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. 管理者に移動して、次の 2 つのルールを作成します。

   * ルール 1：買い物かごに入っている商品の最大 3 品に対して 10 ドルの割引 優先度を設定= *3*.
   * ルール 2：買い物かご内のすべての製品が 50% 割引 優先度を設定= *1*.

1. ストアフロントに移動します。

1. 価格にセットされた商品を 8 個追加= *$51* それぞれをカートに追加します。

1. 買い物かごの割引額を確認します。

<u>期待される結果</u>:

正しく計算されたディスカウントは、期待どおりの$234 です。

* 計算：

  一致する買い物かご価格ルール：ルール 2、ルール 1\
  ルール 2 を適用します（50% オフ）。したがって、割引= $204\
  ルール 1 （3 品目が 10 個）なので、値引= $30 を適用します\
  割引合計=最小（408/2 + 10x3、8 &#42; 51） =最小（204 + 30、8 &#42; 51） = 234 ドル

<u>実際の結果</u>:

最大割引値の計算に使用された数量が間違っているために、割引が誤って$153 と計算されます。これは、買い物かごの商品の金額に関係なく、固定割引金額が適用されるためです。

* 計算：

  一致する買い物かご価格ルール：ルール 2、ルール 1\
  ルール 2 を適用します（50% オフ）。したがって、割引= $204\
  ルール 1 （3 品目が 10 個）なので、値引= $30 を適用します\
  割引合計=最小（204 + 30、3 &#42; 51） = 153 ドル

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
