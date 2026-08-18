---
title: クラウドサイトは低速です
description: この記事では、トラフィック負荷が大きい場合にAdobe Commerce on cloud infrastructure サイトのパフォーマンスを向上させる方法と、この負荷を軽減する方法に関する推奨事項について説明します。
exl-id: 144df36b-6305-4e57-b813-46bbb0ddedda
feature: Cache, Categories, Cloud, Paas
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# クラウドサイトは低速です

この記事では、トラフィック負荷が大きい場合にAdobe Commerce on cloud infrastructure サイトのパフォーマンスを向上させる方法と、この負荷を軽減する方法に関する推奨事項について説明します。

## 影響を受けるバージョンとエディション

* Adobe Commerceオンクラウドインフラストラクチャ（全バージョン）

## イシュー

<u>複製する手順</u>

1. Adobe Commerceストアにアクセス。
1. カテゴリーページを参照します。
1. 商品をカートに追加する。

<u>期待される結果</u>

サイトはレスポンシブで、商品をカートに入れるのは速いです。

<u>実際の結果</u>

サイトの読み込みが遅い、カテゴリーページが速いが買い物かごページが遅い。

## 手順と解決策のデバッグ

パフォーマンスが遅い理由を追跡して修正するには、次の手順に従います。 最初と2番目の手順を切り替えることはできますが、キャッシュ設定の最適化が役立たない場合にのみIPのブロックに進みます。

1. トラフィックの多いページのキャッシュヒット率を確認し、頻繁に更新されるデータの量を減らします。
1. サイト全体のキャッシュヒット率を確認し、一般的なキャッシュ/Fastly設定を確認します。
1. 高いサーバー負荷を引き起こすweb クライアントを特定し、高い負荷を引き起こすIPをブロックします。

以下の段落では、各ステップの詳細を説明します。

### 手順1：トラフィックの多いページのキャッシュヒット率を確認する

トラフィックが多すぎて行き詰まっているサイトを修正するための最初のステップは、ストアのホームページやトップレベルのカテゴリーページなど、トラフィックが最も多いページが適切にキャッシュされていることを確認することです。

これらのページのキャッシュヒット率は、「[cURLを使用したキャッシュの確認](https://docs.fastly.com/guides/debugging/checking-cache#using-curl)」の説明に従って、cURLを使用した`X-Cache` HTTP ヘッダーを確認することで確認できます。 または、お気に入りのweb ブラウザーの開発者ツールバーの「ネットワーク」タブを使用して、同じヘッダーを確認します。

Fastlyは、通常、アプリケーションから取得される応答ヘッダーを尊重します。ただし、ヘッダーがすべて「キャッシュしない」に設定されており、ページが「過去に期限切れになる」場合、Fastlyはページをキャッシュできません。

>[!WARNING]
>
>Fastlyは応答ヘッダーを変更するため、cURLまたはweb ブラウザーでメイン URLを確認しても、アプリケーションによって発行されるヘッダーが必ずしも表示されるわけではありません。 Fastly自体が「キャッシュなし」ヘッダーを使用してweb ブラウザーに応答することは一般的ですが、web アプリケーション自体がキャッシュを許可し、Fastlyがアイテムを適切にキャッシュすることが一般的です。 したがって、「cache-control」および「pragma」ヘッダー情報は、この場合には役に立ちません。

#### トラフィックの多いページのトラブルシューティング

インデックスページのヒット率が低い場合は、そのページに存在する大幅に更新されたデータの量を減らすことによって修正できます。

### 手順2：サイト キャッシュ全体のヒット率を確認する

キャッシュヒット率を確認するには、次の手順に従います。

1. Adobe Commerce on cloud infrastructure環境の[Fastly資格情報](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration)を取得します。
1. 次のLinux/macOS cURL コマンドを実行して、過去30分間のサイトのヒット率を確認し、Fastly資格情報の値にと置き換えます。

   `curl -H "Fastly-Key: " https://api.fastly.com/stats/service//field/hit_ratio?by=minute | json_pp`

   また、時間範囲クエリオプションを`?by=minute`から`?by=hour`または`?by=day`に変更することで、過去1日または1か月の過去のヒット率を確認することもできます。 Fastly キャッシュ統計の取得について詳しくは、Fastly ドキュメントの[&#x200B; クエリオプション &#x200B;](https://docs.fastly.com/api/stats#Query)を参照してください。

   `| json_pp` オプションは、`json_pp` ユーティリティを使用してJSON応答出力をプリプリントします。 a_&#39;json\_ppが見つからない_ エラーが発生した場合は、`json_pp` ユーティリティをインストールするか、別のコマンドラインツールを使用してJSON整形印刷を行います。 または、`| json_pp` パラメーターを削除して、コマンドを再度実行します。 JSON応答出力はフォーマットされていませんが、JSON ビューティファイアを通じて実行してクリーンアップできます。

ヒット率が0.90または90%を超える場合は、ページ全体のキャッシュが機能していることを示します。

ヒット率が0.85または85%未満の場合は、サイト設定の問題を示している可能性があります。または、コンテンツのキャッシュを許可しないサードパーティの拡張機能がインストールされている可能性があります。

#### 全体的なキャッシュヒット率のトラブルシューティング

1. 1時間および1日のヒット率の統計を使用して、ヒット率がいつ減少し始めたかを特定します。 変更をサイトにデプロイした際にヒット率が突然低下した場合は、サイトの読み込みが落ちるまで変更をロールバックすることを検討します。
1. Commerce管理者で、**Stores** > **Configuration** >Advanced > **System** > **Full Page Cache**&#x200B;の設定を確認します。 公開コンテンツ **の値の** TTLが低すぎないようにしてください。
1. VCL スニペット [&#128279;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#upload-vcl-snippets)を アップロードしたことを確認してください。
1. カスタム VCL スニペットを使用する場合は、「パス」または「パイプ」アクションを正しく使用するようにデバッグします。これらは慎重に使用し、少なくとも何らかの条件で使用する必要があります。 詳しくは、開発者ドキュメントの[&#x200B; カスタム Fastly VCL スニペット &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets)を参照してください。

### 手順3：サーバー負荷が高い原因となるweb サイトの特定

次のいずれかの方法を使用して、Adobe Commerce ストアにアクセスするIP アドレスに関する情報を取得できます。

* SSH セッションを介してHTTP アクセスログを確認します。
* Adobe Commerce サポートに連絡して、サイトの負荷が大きいIP アドレスのリストをリクエストしてください。

#### HTTP アクセスログの確認

サイトのアクセスログを確認するには、ローカル開発環境から次のコマンドを実行します。

```bash
magento-cloud log access
```

さらに行を表示

```bash
--lines
```

オプション。例：

```bash
magento-cloud log access --lines=500
```

このログを表示して、リクエストの大部分が特定のIP アドレスから送信されているかどうかを確認できます。 別の方法として、`awk`、`sort`、`uniq`を使用して、ログ内で最も頻繁に発生するIP アドレスを自動的にカウントする方法があります。例えば、次のようになります。

```bash
magento-cloud log access --lines 2000 | awk '{print $1}' | sort | uniq -c | sort
  -nr
```

最初の

```bash
magento-cloud log
```

コマンドが機能しない場合は、SSHでリモートサーバーに接続し、`/var/log/access.log`でログファイルを確認できます

サーバー負荷の高い原因となっているIP アドレスを特定したら、Commerce管理パネルの&#x200B;**Stores** > **Configuration** > ADVANCED > **System** > **Full Page Cache** > **Fastly Configuration** > **Blocking**&#x200B;の下にあるIP ブロックリストを設定して、IP アドレスをブロックできます。

負荷が高いため管理者にアクセスできない場合は、Fastly APIを使用してブロッキングルールを設定できます。

1. 「[APIを使用したACLの操作](https://docs.fastly.com/guides/access-control-lists/working-with-acls-using-the-api) Fastly ドキュメント」の説明に従って、ACLを作成します。
1. `recv` セクションで、ACL\_NAME\_GOES\_HEREを前の手順で作成したACLの名前に置き換えて、次の内容のVCL スニペットを作成します。

   ```
   if( req.http.Fastly-Client-IP ~ ACL_NAME_GOES_HERE ) {
   error 403 "Forbidden";
   }
   ```

IP アドレスのブロックについて詳しくは、GitHubの[Fastly Adobe Commerce モジュールガイド &#x200B;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md)を参照してください。
