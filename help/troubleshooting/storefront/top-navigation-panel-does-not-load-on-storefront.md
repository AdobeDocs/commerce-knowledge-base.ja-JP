---
title: 上部のナビゲーションパネルがストアフロントに読み込まれない
description: この記事では、Varnish Edge Side Includes （ESI）の問題に対する設定ソリューションを提供します。この問題では、Varnish をキャッシュに使用すると、特定のページのコンテンツ（通常は上部のナビゲーションパネル）がストアフロントに表示されません。
exl-id: e7f9b773-1a2d-4c3b-9e1f-a1781fbc898c
feature: Categories, Site Navigation, Storefront, Variables
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 上部のナビゲーションパネルがストアフロントに読み込まれない

この記事では、Varnish Edge Side Includes （ESI）の問題に対する設定ソリューションを提供します。この問題では、Varnish をキャッシュに使用すると、特定のページのコンテンツ（通常は上部のナビゲーションパネル）がストアフロントに表示されません。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.X.X
* すべてのワニスのバージョン

## 問題

<u>前提条件</u>:

Adobe Commerceストア用に Varnish をインストールして設定します。

<u>再現手順</u>:

1. ストアフロントに移動します。
1. ストアページを参照します。

<u>期待される結果</u>:

すべてのコンテンツとすべてのページブロックが正常に読み込まれます。

<u>実際の結果</u>:

カテゴリを含む上部のナビゲーションパネルなどの一部のコンテンツブロックが読み込まれないことがわかります。 代わりに空白が表示されます。

## 原因：

この問題の考えられる理由を次に示します。

* ESI インクルードタグは HTTPS アクセスプロトコルで生成されますが、ワニスは HTTP でのみ機能します。
* ワニスは JSON 内の ESI を処理しません。
* 応答ヘッダーは、Varnish には大きすぎます。処理できません。

## 解決策

問題を解決するには、追加の Varnish 設定を実行し、Varnish を再起動する必要があります。

1. を使用した As a ユーザー `root` 権限がある場合は、Vanish 設定ファイルをテキストエディターで開きます。 を参照してください。 [Varnish システムの設定を変更します。](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish-configure.html#config-varnish-config-sysvcl) このファイルが様々なオペレーティングシステムのどこに格納されているかの情報については、開発者向けドキュメントを参照してください。
1. が含まれる `DAEMON_OPTS variable`、追加： `-p feature=+esi_ignore_https`, `-p  feature=+esi_ignore_other_elements`, `-p  feature=+esi_disable_xml_check`. 次のようになります。

   ```bash
   DAEMON_OPTS="-a :6081 \    -p feature=+esi_ignore_other_elements \    -p feature=+esi_disable_xml_check \    -p feature=+esi_ignore_https \    -T localhost:6082 \    -f /etc/varnish/default.vcl \    -S /etc/varnish/secret \    -s malloc,256m"
   ```

1. 変更を保存し、テキストエディターを終了します。
1. VCL 設定ファイルで、次のパラメータの値を増やして応答ヘッダーを増やします。 `http_resp_hdr_len`, `http_resp_size`, `workspace_backend`. 最後の 2 つの値が類似していることを確認します。
1. これを変更する場合は、を実行する必要があります `service varnish restart` 変更を有効にします。

## 関連資料

* [Varnish と Web サーバーの設定](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish-configure.html#config-varnish-config-sysvcl) 開発者向けドキュメントを参照してください。
* [Varnish ドキュメント](https://varnish-cache.org/docs/5.1/reference/index.html)
