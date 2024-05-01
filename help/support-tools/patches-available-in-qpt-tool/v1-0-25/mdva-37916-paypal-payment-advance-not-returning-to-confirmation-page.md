---
title: 「MDVA-37916:PayPal 支払い処理が進んでいるが、確認ページに戻らない」
description: Adobe Commerce用の MDVA-37916 品質パッチは、PayPal Payments Advanced が支払い後に確認ページに戻らない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.25 がインストールされている場合に利用できます。 パッチ ID は MDVA-37916。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 18d7bb1c-d73a-43f6-90a8-650290dfd114
feature: Orders, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# MDVA-37916: PayPal 支払い詳細支払いが確認ページに戻らない

Adobe Commerce用の MDVA-37916 品質パッチは、PayPal Payments Advanced が支払い後に確認ページに戻らない問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.25 がインストールされています。 パッチ ID は MDVA-37916。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー上のAdobe Commerce 2.3.6-p1

**Adobe Commerce バージョンとの互換性：**
Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.6-2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

PayPal Payments Advanced メソッドを使用する場合、お客様は支払い後に支払い確認ページに移動しません。

<u>再現手順</u>: [スクリーンキャスト](https://assets.adobe.com/public/025d479b-5796-4772-6f3d-adc86306a799)

1. 買い物かごに商品を追加し、チェックアウトページの支払い手順に移動します。
1. を選択 **クレジット カード （Payflow Advanced）** 支払いオプション。
1. クリック **続行** 支払いフォームで iframe を表示します。
1. サンドボックスのクレジットカード詳細を支払いフォームに入力します。
   * カード番号：4444 333 2222 1111 または 4111 1111 1111 111111
   * 有効期限：2023 年 12 月
   * CSC: 123
1. クリック **Pay Now**.

<u>期待される結果</u>:

支払いが処理され、支払いが成功すると、注文確認ページにリダイレクトされます。

<u>実際の結果</u>:

* 注文確認ページにリダイレクトされません。
* しかし、注文はAdobe Commerceで作成されています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe Commerce オンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html)

## 関連資料

サポートナレッジベースの品質向上パッチツールについて詳しくは、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節（サポートナレッジベース）を参照してください。
