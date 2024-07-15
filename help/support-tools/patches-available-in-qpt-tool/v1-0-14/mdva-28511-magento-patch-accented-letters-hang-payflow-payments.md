---
title: 「MDVA-28511：アクセント付き文字がペイフロー支払いをハング」
description: '**Payflow Pro**による支払いが、アクセント記号付きの顧客名で完了しない場合、MDVA-28511 パッチでこの問題を解決します。'
exl-id: ecc827e3-2a1c-4f32-a0e2-9c5792483e7d
feature: Orders, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# MDVA-28511：アクセント付き文字は、Payflow 支払いをハングします

**Payflow Pro** 経由の支払いが、アクセント記号付きの顧客名で完了しない場合、MDVA-28511 パッチでこの問題を解決します。

このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.14 がインストールされている場合に使用できます。 この問題は、Adobe Commerce バージョン 2.3.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用にパッチが作成されます。** Cloud Infrastructure 2.3.5-p1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.3.5 ～ 2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 前提条件 </u>:

**Payflow Pro** クレジットカード支払方法を有効にします。

<u> 再現手順 </u>:

1. 買い物かごに商品を追加し、チェックアウトページに進みます。
1. アクセント付き文字で顧客名を設定します。 （例：**Ãtienne Ãillin**）
1. 支払い手順を続行します。
1. **Payflow Pro** を **クレジットカード** として選択し、クレジットカードの詳細を入力します。
1. **Place Order** ボタンをクリックします。

<u> 期待される結果 </u>:

注文は問題なく完了します。

<u> 実際の結果 </u>:

注文は完了せず、ログには次の例のようなエラーが表示されます。

```php
[2020-06-12 07:50:23] report.CRITICAL: String to be escaped was not valid UTF-8 or could not be converted: �?tienne �?illini [] []
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
