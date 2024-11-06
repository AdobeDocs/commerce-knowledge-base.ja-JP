---
title: クラウドサイトが遅い
description: この記事では、クラウドインフラストラクチャサイト上のAdobe Commerceを、トラフィック負荷の高い環境でのパフォーマンス向上に役立てる方法と、その負荷を軽減する方法について推奨事項を説明します。
exl-id: 144df36b-6305-4e57-b813-46bbb0ddedda
feature: Cache, Categories, Cloud, Paas
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 0%

---

# クラウドサイトが遅い

この記事では、クラウドインフラストラクチャサイト上のAdobe Commerceを、トラフィック負荷の高い環境でのパフォーマンス向上に役立てる方法と、その負荷を軽減する方法について推奨事項を説明します。

## 影響を受けるバージョンとエディション

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

<u> 再現手順 </u>

1. Adobe Commerce ストアにアクセスします。
1. カテゴリページを参照します。
1. 商品を買い物かごに追加します。

<u> 期待される結果 </u>

サイトはレスポンシブで、商品を買い物かごに素早く追加できます。

<u> 実際の結果 </u>

サイトが遅いか、カテゴリページは速いが、買い物かごページは遅い。

## デバッグ手順と解決策

次の手順を実行して、パフォーマンスが低下した理由を突き止め、修正します。 最初と 2 番目のステップを切り替えることができますが、キャッシュ設定の最適化が役に立たない場合にのみ IP のブロックに進みます。

1. トラフィックが多いページのキャッシュヒット率を確認し、頻繁に更新されるデータの量を減らします。
1. サイトキャッシュの全体的なヒット率を確認し、一般的なキャッシュ/Fastly 設定を確認します。
1. サーバー負荷が高い原因となっている Web クライアントを特定し、負荷が高い原因となっているブロック IP を特定します。

次の段落では、各手順の詳細について説明します。

### 手順 1：トラフィック量の多いページのキャッシュヒット率を確認する

トラフィックが多く滞っているサイトを修正する最初の手順は、ストアのホームページやトップレベルのカテゴリページなど、トラフィックが最も多いページが適切にキャッシュされるようにすることです。

これらのページのキャッシュヒット率は、Fastly ドキュメントの [cURL を使用したキャッシュの確認 ](https://docs.fastly.com/guides/debugging/checking-cache#using-curl) で説明されているように、cURL を使用して `X-Cache` HTTP ヘッダーを確認することで確認できます。 または、お気に入りの web ブラウザーの開発者ツールバーにある「ネットワーク」タブを使用して、同じヘッダーを確認します。

Fastly では、通常、アプリケーションからの応答ヘッダーを尊重します。ただし、ヘッダーがすべて「キャッシュしない」に設定され、ページが「過去に期限切れになる」場合、Fastly ではページをキャッシュできません。

>[!WARNING]
>
>Fastly は応答ヘッダーを変更するので、メイン URL を cURL または web ブラウザーで確認しても、アプリケーションから発行されるヘッダーが必ずしも表示されるわけではありません。 Fastly 自体が「キャッシュなし」のヘッダーで web ブラウザーに応答するのが一般的ですが、web アプリケーション自体がキャッシュを許可し、Fastly が項目を適切にキャッシュするのが一般的です。 したがって、「cache-control」ヘッダーと「pragma」ヘッダーの情報は、この場合は役に立ちません。

#### トラフィック量の多いページのトラブルシューティング

インデックスページのヒット率が低い場合は、そのページ上に存在する大幅に更新されたデータの量を減らして修正できます。

### 手順 2：サイトのキャッシュ全体のヒット率を確認する

全体的なキャッシュヒット率を確認するには：

1. クラウドインフラストラクチャ環境のAdobe Commerceの [Fastly 資格情報を取得 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration) します。
1. 次の Linux/macOS cURL コマンドを実行して、過去 30 分間のサイトのヒット率を確認し、とを Fastly 資格情報の値に置き換えます。

   `curl -H "Fastly-Key: " https://api.fastly.com/stats/service//field/hit_ratio?by=minute | json_pp`

   また、時間範囲クエリオプションを `?by=minute` から `?by=hour` または `?by=day` に変更することで、最終日または月にわたる過去のヒット率を確認することもできます。 Fastly のキャッシュ統計の取得について詳しくは、Fastly のドキュメントの [ クエリオプション ](https://docs.fastly.com/api/stats#Query) を参照してください。

   `| json_pp` オプションを使用すると、`json_pp` ユーティリティを使用して JSON 応答出力をプリティプリントできます。 エラー「_&#39;json\_pp not found&#39;_」が発生した場合は、`json_pp` ユーティリティをインストールするか、別のコマンドラインツールを使用して JSON のプリティプリントを行います。 または、`| json_pp` パラメーターを削除して、コマンドを再度実行します。 JSON 応答の出力はフォーマットされていませんが、JSON ビューティファイアを通じて実行するとクリーンアップできます。

ヒット率が 0.90 または 90% を超える場合は、フルページキャッシュが機能していることを示します。

ヒット率が 0.85 または 85% を下回っている場合は、サイトの設定に問題があるか、コンテンツのキャッシュを許可しないサードパーティの拡張機能がインストールされている可能性があります。

#### 全体的なキャッシュヒット率のトラブルシューティング

1. 時間別および日別のヒット率の統計を使用して、ヒット率が低下し始めた時期を識別します。 サイトに変更をデプロイと同時にヒット率が突然低下した場合は、サイトの読み込みが停止するまで変更をロールバックすることを検討してください。
1. Commerce管理者の **ストア**/**設定**/詳細/**システム**/**フルページキャッシュ** で、設定を確認します。 公開コンテンツの **TTL** の値が低く設定されていないことを確認します。
1. [VCL スニペットをアップロード ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#upload-vcl-snippets) したことを確認します。
1. カスタム VCL スニペットを使用する場合は、「pass」または「pipe」アクションを正しく使用するようデバッグしてください。これらは慎重に使用してください。少なくとも、何らかの条件で使用する必要があります。 ヒントについては、開発者向けドキュメントの [Custom Fastly VCL スニペット ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets) を参照してください。

### 手順 3：サーバー負荷が高い原因となっている web サイトを特定する

次のいずれかの方法を使用して、Adobe Commerce ストアにアクセスする IP アドレスに関する情報を取得できます。

* SSH セッションで HTTP アクセスログを確認します。
* サイトに大きな負荷がかかる IP アドレスのリストをリクエストするには、Adobe Commerce サポートにお問い合わせください。

#### HTTP アクセスログを確認します

サイトのアクセスログを表示するには、ローカル開発環境から次のコマンドを実行します。

```bash
magento-cloud log access
```

で他の行を表示

```bash
--lines
```

例えば、次のようなオプションがあります。

```bash
magento-cloud log access --lines=500
```

このログを確認すると、リクエストの大部分が特定の IP アドレスから送信されているかどうかを確認できます。 もう 1 つの方法は、`awk`、`sort` および `uniq` を使用して、次のようにログ内で最も頻繁に発生する IP アドレスを自動的にカウントすることです。

```bash
magento-cloud log access --lines 2000 | awk '{print $1}' | sort | uniq -c | sort
  -nr
```

次の場合

```bash
magento-cloud log
```

コマンドが動作しません。SSH を使用してリモート サーバーに接続し、`/var/log/access.log` にあるログ ファイルを確認してください

サーバーの負荷が高い原因となる IP アドレスを特定したら、Commerce管理パネルの **ストア**/**設定**/詳細/**システム**/**フルページキャッシュ**/**Fastly 設定**/**ブロッキング** で IPブロックリストを行うことで、それらのアドレスをブロックできます。

高負荷が原因で管理者にアクセスできない場合は、Fastly API を使用してブロッキングルールを設定できます。

1. [API を使用した ACL の操作 ](https://docs.fastly.com/guides/access-control-lists/working-with-acls-using-the-api)Fastly ドキュメントの説明に従って、ACL を作成します。
1. `recv` のセクションで、次の内容の VCL スニペットを作成します。ACL\_NAME\_GOES\_HEREは、前の手順で作成した ACL の名前に置き換えます。

   ```
   if( req.http.Fastly-Client-IP ~ ACL_NAME_GOES_HERE ) {
   error 403 "Forbidden";
   }
   ```

IP アドレスのブロックについて詳しくは、GitHub の [Fastly Adobe Commerce モジュールガイド ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) を参照してください。
