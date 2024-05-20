---
title: サイトおよび API のパフォーマンスの低下
description: この記事では、「debug.log」の書き込みに長時間かかることで発生したサイトと API のパフォーマンスの低下に関連する、Adobe Commerce on cloud infrastructure 2.2.1 の既知の問題に対するパッチを提供します。
exl-id: b71816cd-f580-4c80-9694-585ed051a56d
feature: REST, Observability
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# サイトおよび API のパフォーマンスの低下

この記事では、書き込みに長い時間がかかることが原因で発生したサイトと API のパフォーマンスの低下に関連する、Adobe Commerce on cloud infrastructure 2.2.1 の既知の問題に対するパッチを提供します `debug.log`.

## 問題

サイトのパフォーマンスが遅い。 API 操作の実行に時間がかかる（例： `PUT` メソッド。 New Relicを使用した操作を詳しく見ると、ほとんどのメモリと CPU は、に書き込むことで消費されています。 `/var/log/debug.log`.

## 解決策

この問題を解決するには、パッチを適用します。 このパッチは、ログ、支払い、発送方法のログを分割して個別のファイルに書き込みます。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-8371\_EE\_2.2.1\_COMPOSER\_v2.patch のダウンロード](assets/MDVA-8371_EE_2.2.1_COMPOSER_v2.patch.zip)

### 互換性のあるAdobe Commerce バージョン

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.2.1 上のAdobe Commerce

このパッチは、次のAdobeバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.0、2.2.2、2.2.3
* Adobe Commerce オンプレミス 2.2.0、2.2.2、2.2.3

## パッチの適用方法

参照： [Adobe Commerceが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 手順については、サポートナレッジベースを参照してください。

## 添付ファイル
