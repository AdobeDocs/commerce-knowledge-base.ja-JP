---
title: デフォルトのVarnish設定を変更する必要が生じた503 エラーのトラブルシューティング
description: この記事では、特定のVarnish Cacheのデフォルト値がストアに十分ではないために発生する503 エラーのトラブルシューティングに関するソリューションを提供します。
exl-id: 3f001cc9-b19a-4dee-bff0-fc8ba89e2646
feature: Cache, Categories
role: Admin
source-git-commit: be0c72a1759ba172666c7c9409c65a1a388e3f11
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# デフォルトのVarnish設定を変更する必要が生じた503 エラーのトラブルシューティング

この記事では、特定のVarnish Cacheのデフォルト値がストアに十分ではないために発生する503 エラーのトラブルシューティングに関するソリューションを提供します。

## イシュー

Adobe Commerceで使用されるキャッシュタグの長さがVarnishのデフォルトの8192 バイトを超える場合、ブラウザーにHTTP 503 （バックエンドフェッチ失敗）エラーが表示されます。 エラーは次のように表示される場合があります。*「エラー503 バックエンドの取得に失敗しました。 バックエンド フェッチに失敗しました&quot;*

## Solution

この問題を解決するには、Varnish設定ファイルの`http_resp_hdr_len` パラメーターのデフォルト値を増やします。 `http_resp_hdr_len` パラメーターは、32768 バイトのデフォルトの応答サイズの合計を&#x200B;*以内の最大ヘッダー長*&#x200B;を指定します。

>[!NOTE]
>
>`http_resp_hdr_len`の値が32Kを超える場合は、`http_resp_size` パラメーターを使用してデフォルトの応答サイズも増やす必要があります。

1. `root`権限を持つユーザーとして、Vanish設定ファイルをテキストエディターで開きます。
   * CentOS 6: `/etc/sysconfig/varnish`
   * CentOS 7: `/etc/varnish/varnish.params`
   * Debian: `/etc/default/varnish`
   * Ubuntu: `/etc/default/varnish`
1. `http_resp_hdr_len` パラメーターを検索します。
1. パラメーターが存在しない場合は、`thread_pool_max`の後に追加します。
1. `http_resp_hdr_len`を、最大カテゴリの製品数に21を掛けた値に設定します。 （製品タグの長さは約21文字です）。 例えば、最大のカテゴリに3,000個の商品がある場合、値を65536 バイトに設定すると機能します。 例：`-p http_resp_hdr_len=65536 \`
1. `http_resp_size`を、増加した応答ヘッダーの長さに対応する値に設定します。    例えば、ヘッダー長の増加とデフォルトの応答サイズの合計を使用すると、適切な開始点となります（例：65536 + 32768 = 98304）: `-p http_resp_size=98304`。 スニペットは次のようになります。

   ```
   # DAEMON_OPTS is used by the init script.
   DAEMON_OPTS="-a ${VARNISH_LISTEN_ADDRESS}:${VARNISH_LISTEN_PORT} \
       -f ${VARNISH_VCL_CONF} \
       -T ${VARNISH_ADMIN_LISTEN_ADDRESS}:${VARNISH_ADMIN_LISTEN_PORT} \
       -p thread_pool_min=${VARNISH_MIN_THREADS} \
       -p thread_pool_max=${VARNISH_MAX_THREADS} \
       -p http_resp_hdr_len=65536 \
       -p http_resp_size=98304 \
       -p workspace_backend=98304 \
       -S ${VARNISH_SECRET_FILE} \
       -s ${VARNISH_STORAGE}" \
   ```

## ヘルスチェックのタイムアウト {#health-check-timeouts}

Varnishがキャッシングアプリケーションとして設定されている間にキャッシュを無効にし、Adobe Commerceがデベロッパーモードの間に、管理者にログインできなくなる可能性があります。

この問題は、既定のヘルスチェックの値が`timeout`で2秒であるため発生する可能性があります。 ヘルスチェックがすべてのヘルスチェック要求に関する情報を収集し、結合するのに2秒以上かかる場合があります。 この問題が10回のヘルスチェックのうち6回で発生した場合、Adobe Commerce サーバーは異常と見なされます。 Varnishは、サーバーが正常でない場合に古いコンテンツを配信します。

管理者はVarnishを通じてアクセスするため、管理者にログインしてキャッシュを有効にすることはできません（Adobe Commerceが再び正常になる場合を除く）。 ただし、次のコマンドを使用してキャッシュを有効にできます。

```bash
$ bin/magento cache:enable
```

コマンドラインの使用について詳しくは、[&#x200B; コマンドライン設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli)を参照してください。

