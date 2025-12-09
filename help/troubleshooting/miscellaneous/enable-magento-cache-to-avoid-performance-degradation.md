---
title: パフォーマンスの低下を避けるためにキャッシュを有効にする
description: この記事では、特定のAdobe Commerce キャッシュタイプが無効になっていることが原因で発生するサイトの速度の問題を解決する方法について説明します。
exl-id: e4e5a753-efa3-4552-aaf6-28e44efcfa5b
feature: Cache, Observability
role: Developer
source-git-commit: d9985fecdafa63882f8411b32e296cc47583c93d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# パフォーマンスの低下を避けるためにキャッシュを有効にする

この記事では、特定のAdobe Commerce キャッシュタイプが無効になっていることが原因で発生するサイトの速度の問題を解決する方法について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x
* Adobe Commerce オンプレミス 2.2.x、2.3.x

## 問題

パフォーマンスの低下が見られます。 例えば、チェックアウト ページの読み込みに時間がかかったり、New Relicで Apdex 値が減少したりします。

## 原因：

パフォーマンスが低下する理由の 1 つは、特定のAdobe Commerce キャッシュタイプが無効になっていることです。

## 解決策

1. 最初に、Adobe Commerce キャッシュのステータスをチェックして、これが問題であるかどうかを確認します。 この場合は、環境に [SSH](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh) 接続し、次のコマンドを実行します。

   ```bash
   php bin/magento cache:status
   ```

   これにより、各キャッシュタイプのステータスが表示されます（無効の場合は「0」、有効の場合は「1」）。 または、この情報を `app/etc/env.php` ファイルで取得できます。

1. 無効なキャッシュタイプを調べます。 Adobeから別のガイダンスを受けない限り、すべてのAdobe Commerce キャッシュタイプを有効にする必要があります。 サードパーティの拡張機能では、Adobe Commerceのキャッシュを無効にする必要はありません。
1. 調査により、一部のキャッシュタイプが誤って無効になっていることが確認された場合は、各キャッシュタイプに対して次のコマンドを実行して、それらを有効にします。`php bin/magento cache:enable <your_disabled_cache_type>`

特定のAdobe Commerce キャッシュタイプを無効にできるか無効にすべきかとの懸念や質問がある場合は、[Adobe Commerce サポートにお問い合わせ ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)、レコメンデーションを求めてください。

## 関連資料

開発者向けドキュメントのAdobe Commerce キャッシュのドキュメント：

* [Adobe Commerce キャッシュの概要 ](https://developer.adobe.com/commerce/frontend-core/guide/caching/)
* [ キャッシュの管理 ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-cache)

パフォーマンスの問題が発生するその他の理由と解決策：

* [ サイトのパフォーマンスを向上させるには、Adobe Commerce バナーの出力を無効にします ](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26909)
* [MySQL テーブルが大きすぎます ](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26945)
* [パフォーマンスが遅く、動作が遅く、長時間実行されるクローン](/help/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.md)