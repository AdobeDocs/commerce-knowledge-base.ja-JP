---
title: 接触チャネルクロークにより、サイトにアクセスできない
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceのステージングまたは実稼動サイトのストアフロントや管理者がアクセスできない場合の解決策を説明します。
exl-id: 4412d744-3066-4f78-bc45-8149614ce455
feature: Products
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 接触チャネルクロークにより、サイトにアクセスできない

この記事では、クラウドインフラストラクチャー上のAdobe Commerceのステージングまたは実稼動サイトのストアフロントや管理者がアクセスできない場合の解決策を説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.x、2.4.x

## 問題

https:/&#x200B;/mydomain.com.c.&lt;projectid>.magento.cloud/にはアクセスできなくなりました。

<u>再現手順：</u>

1. プロジェクトにログインします。
1. クリック **プロジェクトへのアクセス** URL と SSH のリストについては、を参照してください。

<u>実際の結果：</u>

次のエラーでページの読み込みに失敗します。

*NET::ERR\_CERT\_INVALID*  *TLS アラート、不正な証明書（554）:*

<u>期待される結果：</u>

ページが正常に読み込まれました。

## 原因：

オリジンクロークが有効になっているので、オリジンに直接アクセスできなくなりました。

オリジンクロークは、DDoS 攻撃を防ぐために、クラウドインフラストラクチャ（オリジン）に送信される非 Fastly トラフィックをAdobe Commerceがブロックできるようにするセキュリティ機能です。

## 解決策

* クラウドサイトがライブの場合は、https://mydomain.com/に切り替えます。
* アクティブなサイト（クラウド以外）がある場合は、https://mydomain.com/ ドメインを使用してサブドメインを設定します `mcprod.mydomain.com` を更新します **ベース URL** 対象： *https://mcprod.mydomain.com* 代わりに、 [dns を Fastly に指定する](https://devdocs.magento.com/cloud/cdn/configure-fastly.html#update-dns-configuration-with-development-settings).

## 関連資料

[Fastly オリジンクローク有効化に関する FAQ](/help/faq/general/fastly-origin-cloaking-enablement-faq.md) サポートナレッジベースで。
