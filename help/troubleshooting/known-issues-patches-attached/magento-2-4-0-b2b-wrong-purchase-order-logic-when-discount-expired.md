---
title: 「Adobe Commerce 2.4.0 B2B：割引期限切れ時の間違った発注書ロジック」
description: この記事では、Adobe Commerce 2.4.0 B2B で適用されていない発注書（PO） ディスカウントの既知の問題に対するパッチを提供します。 発注が承認処理中に失効した割引コードで発注された場合、承認済の受注には割引は反映されません。
exl-id: 3ef41655-c31e-4e9c-8985-fa1b4fd53170
feature: B2B, Orders, Payments, Personalization, Purchase Orders
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 B2B：値引の失効時の誤った発注ロジック

この記事では、Adobe Commerce 2.4.0 B2B で適用されていない発注書（PO） ディスカウントの既知の問題に対するパッチを提供します。 発注が承認処理中に失効した割引コードで発注された場合、承認済の受注には割引は反映されません。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.0

## 問題

<u>前提条件</u>：割引クーポンが作成され、発注が自動的に処理されない承認ルールが存在する。

<u>再現手順：</u>

1. ディスカウントが適用された発注を行います。
1. 割引クーポンを無効にします。
1. マネージャーとして発注を承認します。
1. 結果として作成された注文を確認します。

<u>期待される結果：</u>

注文は割引合計で作成されます。

<u>実際の結果：</u>

注文が全額作成されます。

## 解決策

この記事で提供されているパッチを適用します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[B2B-709-composer.patch](assets/B2B-709-composer.patch.zip)

このパッチは、次の場所からダウンロードすることもできます。 `.git` および `.composer` 、形式 [Adobe Commerce ダウンロード](https://magento.com/tech-resources/download) ページ、下 **パッチ** 左の列のナビゲーションで上書きできます。 XXX パッチを検索します。

## パッチの適用方法

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 手順については、サポートナレッジベースを参照してください。
