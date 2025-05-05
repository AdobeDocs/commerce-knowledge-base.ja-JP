---
title: 接触チャネルクロークにより、サイトにアクセスできない
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceのステージングまたは実稼動サイトのストアフロントや管理者がアクセスできない場合の解決策を説明します。
exl-id: 4412d744-3066-4f78-bc45-8149614ce455
feature: Products
role: Developer
source-git-commit: b58e182c64b3fad508145d9078619ddbe0e2b887
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 接触チャネルクロークにより、サイトにアクセスできない

この記事では、クラウドインフラストラクチャー上のAdobe Commerceのステージングまたは実稼動サイトのストアフロントや管理者がアクセスできない場合の解決策を説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.x、2.4.x

## 問題

https:/&#x200B;/mydomain.com.c.&lt;projectid>.magento.cloud/にはアクセスできなくなりました。

<u> 再現手順：</u>

1. プロジェクトにログインします。
1. URL と SSH のリストを表示するには、「**プロジェクトにアクセス**」をクリックします。

<u> 実績：</u>

次のエラーでページの読み込みに失敗します。

*NET::ERR\_CERT\_INVALID**TLS アラート、不正な証明書（554）:*

<u> 期待される結果：</u>

ページが正常に読み込まれました。

## 原因：

オリジンクロークが有効になっているので、オリジンに直接アクセスできなくなりました。

オリジンクロークは、DDoS 攻撃を防ぐために、クラウドインフラストラクチャ（オリジン）に送信される非 Fastly トラフィックをAdobe Commerceがブロックできるようにするセキュリティ機能です。

## 解決策

* クラウドサイトがライブの場合は、https://mydomain.com/に切り替えます。
* アクティブなサイト（クラウド以外）がある場合は、https://mydomain.com/ ドメインを使用してサブドメイン `mcprod.mydomain.com` を設定し、**ベース URL** を *https://mcprod.mydomain.com* に更新して、[DNS を Fastly に指定 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#update-dns-configuration-with-development-settings) ます。

## 関連資料

* [Fastly オリジンクローキングのイネーブルメントに関する FAQ](/help/faq/general/fastly-origin-cloaking-enablement-faq.md) をサポートナレッジベースに掲載しています
* サポートナレッジベースの [ 新しいドメインを設定するためのチェックリスト ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/how-to/checklist-for-setting-up-a-new-domain)
