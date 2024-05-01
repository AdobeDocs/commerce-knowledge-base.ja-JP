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

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.14 がインストールされています。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

B2B バージョン 1.2 を使用したクラウドインフラストラクチャー 2.3.2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.3.5-p2、2.4.0、2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>前提条件</u>:

B2B を含む新しいAdobe Commerce インスタンスをインストールします。

<u>再現手順</u>:

1. に移動 **ストア /設定/一般/ B2B 機能** および有効化 **会社** および **B2B の見積もり**.
1. を使用して、さらに 2 つの web サイトを作成 **ストア** および **レビューを保存** （合計で 3 つの web サイトが必要です。 *ベース*, *website2*, *web サイト 3*）に設定します。
1. シンプルな製品を作成して、次のユーザーにのみ割り当てる： *web サイト 3*.
1. に移動 **ストア/すべてのストア** およびを設定 *web サイト 3* as **default**.
1. フロントエンドに移動し、に新しい会社を作成します *web サイト 3*.
1. 以前に作成した製品を買い物かごに追加し、新しい交渉可能な見積もりを作成します。
1. に移動 **ストア/すべてのストア** を設定して「*ベース*」の web サイトを **default**.
1. に移動 **「営業」 > 「見積」 > 「以前に作成した見積をオープン」** そして同じ製品を追加してみてください。

<u>期待される結果</u>:

管理者ユーザーは、期待どおりに同じ製品を見積もりに追加できます。

<u>実際の結果</u>:

管理者ユーザーは同じ製品を見積もりに追加できず、次のエラーメッセージが表示されます。

```php
This product is assigned to another website.
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
