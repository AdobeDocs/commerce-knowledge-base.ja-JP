---
title: 「MDVA-32694 パッチ：見積もりに製品を追加する際の問題」
description: MDVA-32694 パッチを使用すると、デフォルト以外の Web サイトで作成された交渉可能な見積もりに Admin で有効な製品を追加できない問題を解決できます。
exl-id: 964abbbd-c8b1-4645-a393-7283f52e94ff
feature: Products, Quotes
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# MDVA-32694 パッチ：見積もりに製品を追加する際の問題

MDVA-32694 パッチを使用すると、デフォルト以外の Web サイトで作成された交渉可能な見積もりに Admin で有効な製品を追加できない問題を解決できます。

このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.14 がインストールされている場合に使用できます。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

B2B バージョン 1.2 を使用したクラウドインフラストラクチャー 2.3.2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.3.5-p2、2.4.0、2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 前提条件 </u>:

B2B を含む新しいAdobe Commerce インスタンスをインストールします。

<u> 再現手順 </u>:

1. **STORES/設定/一般/B2B 機能** に移動し、「**Company**」と「**B2B quote**」を有効にします。
1. **stores** および **storeviews** を使用して、さらに 2 つの web サイトを作成します（合計で、*base*、*website2*、*website3* の 3 つの web サイトが必要です）。
1. シンプルな製品を作成して、*website3* にのみ割り当てます。
1. **ストア/すべてのストア** に移動し、*website3* を **デフォルト** として設定します。
1. フロントエンドに移動し、*website3* で新しい会社を作成します。
1. 以前に作成した製品を買い物かごに追加し、新しい交渉可能な見積もりを作成します。
1. **ストア/すべてのストア** に移動し、「*base*」 Web サイトを **デフォルト** に戻します。
1. **SALES/見積もり/作成した以前の見積もりを開く** に移動して、同じ製品を追加してみてください。

<u> 期待される結果 </u>:

管理者ユーザーは、期待どおりに同じ製品を見積もりに追加できます。

<u> 実際の結果 </u>:

管理者ユーザーは同じ製品を見積もりに追加できず、次のエラーメッセージが表示されます。

```php
This product is assigned to another website.
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
