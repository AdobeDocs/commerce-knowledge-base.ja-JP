---
title: デフォルトの Varnish 設定を変更する必要があるために発生した 503 エラーのトラブルシューティング
description: この記事では、特定の Varnish Cache のデフォルト値がストアに十分でないことが原因で発生した 503 エラーのトラブルシューティングに対する解決策を提供します。
exl-id: 3f001cc9-b19a-4dee-bff0-fc8ba89e2646
feature: Cache, Categories
role: Admin
source-git-commit: 9c5e993b69a98865a1142110625252da848eae04
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# デフォルトの Varnish 設定を変更する必要があるために発生した 503 エラーのトラブルシューティング

この記事では、特定の Varnish Cache のデフォルト値がストアに十分でないことが原因で発生した 503 エラーのトラブルシューティングに対する解決策を提供します。

## 問題

Adobe Commerceで使用されるキャッシュタグの長さが Varnish のデフォルトの 8192 バイトを超えている場合、ブラウザーに HTTP 503 （バックエンドの取得に失敗しました）エラーが表示される可能性があります。 エラーは次のように表示されることがあります。 *「エラー 503 バックエンドの取得に失敗しました。 バックエンドの取得に失敗しました」*

## 解決策

この問題を解決するには、のデフォルト値を増やします `http_resp_hdr_len` varnish 設定ファイルのパラメータ。 この `http_resp_hdr_len` パラメーターは、ヘッダーの最大長を指定します *内* デフォルトの応答サイズの合計（32768 バイト）。

>[!NOTE]
>
>次の場合 `http_resp_hdr_len` 値が 32,000 を超える場合は、を使用してデフォルトの応答サイズを増やす必要もあります。 `http_resp_size` パラメーター。

1. を使用した As a ユーザー `root` 権限を持つ場合は、Vanish 設定ファイルをテキストエディターで開きます。
   * CentOS 6: `/etc/sysconfig/varnish`
   * CentOS 7: `/etc/varnish/varnish.params`
   * Debian: `/etc/default/varnish`
   * Ubuntu: `/etc/default/varnish`
1. を検索 `http_resp_hdr_len` パラメーター。
1. パラメーターが存在しない場合は、の後に追加します `thread_pool_max` .
1. を設定 `http_resp_hdr_len` 最大カテゴリの製品数に 21 を掛けた値。 （1 つの製品タグの長さは約 21 文字です。）    例えば、最大のカテゴリの製品が 3,000 個ある場合、値を 65536 バイトに設定しても機能します。    例：    ```conf    -p http_resp_hdr_len=65536 \    ```
1. を `http_resp_size` 増加した応答ヘッダー長に対応する値に設定します。    例えば、ヘッダーの長さとデフォルトの応答サイズの増加の合計を使用することは、出発点として適切です（例：65536 + 32768 = 98304）。 `-p http_resp_size=98304`. スニペットは次のとおりです。

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

Varnish がキャッシュアプリケーションとして設定されていて、Adobe Commerceがデベロッパーモードの間にキャッシュを無効にすると、管理者にログインできなくなる可能性があります。

このような状況が発生する可能性があるのは、デフォルトのヘルスチェックにが含まれているからです。 `timeout` 値は 2 秒です。 ヘルスチェックリクエストごとにヘルスチェックが情報を収集して結合するまで、2 秒以上かかる場合があります。 これが 10 件中 6 件のヘルスチェックで発生した場合、Adobe Commerce サーバーは正常ではないと見なされます。 ワニスは、サーバーが正常でない場合に古いコンテンツを提供します。

管理者は Varnish を通じてアクセスするので、（Adobe Commerceが再び正常にならない限り）管理者にログインしてキャッシュを有効にすることはできません。 ただし、次のコマンドを使用してキャッシュを有効にすることができます。

```bash
$ bin/magento cache:enable
```

コマンド ラインの使用方法の詳細については、を参照してください。 [コマンドライン設定の基本を学ぶ](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands.html).
