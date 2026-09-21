---
title: キャッシュを有効にしてパフォーマンスの低下を回避
description: この記事では、Adobe Commerceの特定のキャッシュの種類が無効になることでサイトの動作が遅くなる問題を解決する方法について説明します。
exl-id: e4e5a753-efa3-4552-aaf6-28e44efcfa5b
feature: Cache, Observability
role: Developer
source-git-commit: 42aa1d4ef3540d4eb9682627dc5bf1dd14091dc3
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%
---
# キャッシュを有効にしてパフォーマンスの低下を回避

この記事では、Adobe Commerceの特定のキャッシュの種類が無効になることでサイトの動作が遅くなる問題を解決する方法について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure 2.2.x、2.3.x
* Adobe Commerce オンプレミス 2.2.x、2.3.x

## イシュー

パフォーマンスが低下しています。 例えば、チェックアウトページの読み込みが遅い、New RelicでApdex値が減少するといった具合です。

## 原因

パフォーマンスが低下する理由の1つは、特定のAdobe Commerce キャッシュの種類が無効になっている可能性があります。

## Solution

1. まず、Adobe Commerce キャッシュのステータスを確認して、これが問題であるかどうかを確認します。 このために、[SSHをお使いの環境](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh)に送信し、次のコマンドを実行します。

   ```bash
   php bin/magento cache:status
   ```

   これにより、各キャッシュタイプのステータスが表示されます（無効の場合は「0」、有効の場合は「1」）。 または、`app/etc/env.php` ファイルでこの情報を取得できます。

1. 無効なキャッシュタイプを調べます。 Adobeから別のガイダンスを受けない限り、すべてのAdobe Commerce キャッシュタイプを有効にする必要があります。 サードパーティの拡張機能では、Adobe Commerce キャッシュを無効にする必要はありません。
1. 調査で一部のキャッシュの種類が誤って無効になっていることが確認された場合は、キャッシュの種類ごとに次のコマンドを実行して有効にします：`php bin/magento cache:enable <your_disabled_cache_type>`

特定のAdobe Commerce キャッシュの種類を無効にできるか無効にすべきかについての懸念や質問がある場合は、[Adobe Commerce サポート &#x200B;](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)にお問い合わせください。

## 関連トピックス

Adobe Commerceのキャッシュドキュメントをご覧ください。

* [Adobe Commerce キャッシュの概要](https://developer.adobe.com/commerce/frontend-core/guide/caching)
* [キャッシュの管理](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-cache)

パフォーマンスの問題とその解決策のその他の考えられる理由：

* [Adobe Commerce Banner出力を無効にして、サイトパフォーマンスを向上させる](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26909)
* [MySQL テーブルが大きすぎます](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26945)
* [遅いパフォーマンス、遅い動作のcron](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-42802)
