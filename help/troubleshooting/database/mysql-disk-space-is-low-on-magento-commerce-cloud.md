---
title: 「クラウドインフラストラクチャー上のAdobe Commerceの [!DNL MySQL] ディスク領域が不足しています」
description: この記事では、クラウドインフラストラクチャ上でAdobe Commerce用のスペースが非常に少ない場合や、スペースがない場合のソリュ  [!DNL MySQL]  ションについて説明します。 サイトの停止、買い物かごに製品を追加できない、データベースに接続できない、データベースにリモートでアクセスできない、ノードに SSH 接続できないなどの症状が発生する可能性があります。 また、Galera、環境の同期、PHP、データベース、および以下に示すデプロイメントエラーも症状に含まれます。 [ ソリューション ] （https://support.magento.com/hc/en-us/articles/360058472572#solution）をクリックすると、ソリューション セクションに直接ジャンプします。
exl-id: 788c709e-59f5-4062-ab25-5ce6508f29f9
feature: Catalog Management, Categories, Cloud, Paas, Services
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---

# クラウドインフラスト [!DNL MySQL] クチャ上のAdobe Commerceのディスク領域が少ない

この記事では、クラウドインフラストラクチャー上のAdobe Commerceでスペースが非常に少ない場合や、スペースがない場合のソリュ [!DNL MySQL] ションについて説明します。 サイトの停止、買い物かごに製品を追加できない、データベースに接続できない、データベースにリモートでアクセスできない、ノードに SSH 接続できないなどの症状が発生する可能性があります。 また、Galera、環境の同期、PHP、データベース、および以下に示すデプロイメントエラーも症状に含まれます。 [ ソリューション ](https://support.magento.com/hc/en-us/articles/360058472572#solution) をクリックして、ソリューションセクションに直接ジャンプします。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce 2.3.0-2.3.6-p1、2.4.0-2.4.2

## 問題

データベースが大きすぎます。 この症状には、データベース接続の切断、データベースのアップロードエラー、その他の様々な問題が含まれる場合があります。

発生する可能性のあるエラー：

ガレラ：

* *SQLSTATE\[08S01\]：通信リンク エラー：1047 WSREP はまだアプリケーションで使用するノードを準備していません*   *読み込みエラー：*
* *SQLSTATE\[HY000\]：一般的なエラー：1180 エラー 5 「入力/出力エラー」が発生しました*
* *SQLSTATE\[08S01\]：通信リンク エラー：1047 WSREP はまだアプリケーションで使用するノードを準備していません*

環境同期エラー：

* *SQLSTATE：一般的なエラー：1180 COMMIT 中にエラー 5 「Input/output error」が発生する*

PHP エラー：

* *php: PDO::\_\_construct （）: サーバ [!DNL MySQL] 使用できなくなりました。*
* *php エラー：PDO::\_\_construct （）: greeting パケットの読み込み中にエラーが発生しました。 PID=NNNN.*
* *エラー 2013 （HY000）: &#39;初期通信パケットの読み取り&#39;で [!DNL MySQL] サーバーへの接続が失われました。システム エラー：0 &quot;内部エラー/チェック （システム エラーではありません）&quot;。*

データベース エラー：

* *Error\_code: 1114*
* *InnoDB: FTS 補助インデックス テーブルにワード ノードを書き込み中にエラー（ディスク領域不足）が発生しました。*
* *SQLSTATE\[HY000\]：一般エラー：2006 [!DNL MySQL] サーバーが停止しました*
* *\[ERROR\] スレーブ SQL: クエリの&#39;テーブル `<table\_name>` がいっぱいです&#39; エラー*
* *ユニット mysql.service が失敗状態になりました。*
* *エラー：&#39;ソケット「/var/run/mysqld/mysqld.sock」を使用してローカル [!DNL MySQL] サーバーに接続できません（111 &quot;接続が拒否されました）&#39;*
* *1205 ロック待機のタイムアウトを超えています。トランザクションを再度開始してください。クエリは次のとおりです：INSERT INTO \&#39;cron\_schedule\&#39; （\&#39;job\_code\&#39;, \&#39;status\&#39;, \&#39;created\_at\&#39;, \&#39;scheduled\_at\&#39;）値（?, ?, `YYYY-02-07 HH:MM:SS`, `YYYY-MM-DD HH:MM:SS`）*

展開エラー：

* *E: コマンド「\[&#39;sudo&#39;, &#39;-u&#39;, `<environment name>`, &#39;bash&#39;, &#39;-c&#39;, &#39;/etc/platform/`<environment name>`/post\_deploy.sh&#39;\]」がゼロ以外の終了ステータス 255 を返しました*
* *E: コマンド &#39;\[&#39;ssh&#39;, u`<node IP address>`, &#39;sudo /usr/bin/sv -w 30 restart site-`<environment name>`g-nginx&#39;\]&#39;がゼロ以外を返しました*
* *スキーマをアップグレードしています… SQLSTATE\[HY000\]：一般エラー：1114 テーブル `<table\_name>` がいっぱいです*
* *SQLSTATE\[HY000\]：一般エラー：3 ファイルの書き込み中にエラーが発生しました。/`<environment name>`/\#*
* *W: `<filename>` （エラーコード：28 「デバイスに空き領域がありません」）**インデックス作成エラー（/tmp の孤立した一時.ibd ファイルと共に）:*
* *カタログルールインデクサーで例外がスローされる。 一時テーブルは、その後にクリーンアップされず、現在の [!DNL MySQL] マスターノードのディスクに書き込まれます*

<u> 再現手順 </u>:

`/data/mysql` （またはデータ・ストレージが構成されてい [!DNL MySQL] 場所）がいっぱいかどうかを確認する方法の 1 つは、CLI で次のコマンドを実行する方法です。

```bash
df -h
```

ディスク上の空きメモリが 10% 未満であ [!DNL MySQL] ことが、システム停止の主な指標です。

## 原因：

inode が不足している、使用可能なストレージ領域が不足している、一時テーブルを生成する不適切なクエリなど、様々な問題が原因で、`/data/mysql` マウントがいっぱいになる可能性があります。

## 解決策

[!DNL MySQL] を元の軌道に戻す（または停止するのを防ぐ）ための即時の手順があります。大きなテーブルをフラッシュして、スペースを解放します。

しかし、長期的なソリューションとしては、より多くのスペースを割り当て、[ 注文/請求書/出荷アーカイブ ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html) 機能の有効化など、[ データベースのベストプラクティス ](https://docs.magento.com/user-guide/sales/order-archive.html) に従うことになります。

以下は、迅速なソリューションと長期的なソリューションの両方の詳細です。

### inode のチェックと解放

十分な数の使用可能な inode があることを確認します。 これを行うには、次のコマンドを実行します。

```bash
df -i
```

出力は次のようになります。

```bash
Filesystem Inodes   Used   Free Use% Mounted on
/dev/nvme2n1 655360    1695  653665    1% /data/mysql
```

使用 % が 70% 未満であることを確認します。 inode はファイルと相関関係があります。 パーティションからファイルを削除すると、inode が解放されます。

### ストレージスペースの確認と解放

使用可能なストレージスペースを確認します。 そのためには、次を実行します。

```bash
df -k
```

出力は次のようになります。

```bash
Size Used Avail Use% Mounted on·
       50G 49G 95M 100% /data/mysql
```

使用率 % が 70% を超える場合は、領域を解放または追加するために対処する必要があります。

### サイズの大きい `ibtmp1` ファイルの確認

各ノードの `/data/mysql` にある大きな `ibtmp1` ファイルを確認します。このファイルは、一時テーブルのテーブル領域です。 一時テーブルを生成する不正なクエリがある場合、それらは `ibtmp1` ファイルに含まれます。 このファイルは、データベースが再起動されたときにのみ削除されます。 使用可能なすべての領域を占有している場合は、データベースを再起動する必要があります。 無効なクエリがある場合は、再度作成されます。

### 大きいテーブルのフラッシュ

>[!WARNING]
>
>操作を実行する前にデータベースバックアップを作成し、サイトの負荷が高い期間は避けることを強くお勧めします。 開発者向けドキュメントの [ データベースのダンプ ](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump) を参照してください。

大きなテーブルがあるかどうかを確認し、フラッシュできるテーブルがあるかどうかを検討します。 これをプライマリ（ソース）ノードで行います。

例えば、レポートを含むテーブルは通常フラッシュできます。 大きいテーブルの検索方法について詳しくは、[ 大きいテーブルの検索  [!DNL MySQL]  の記事を参照してください ](/help/how-to/general/find-large-mysql-tables.md)

巨大なレポートテーブルがない場合は、Adobe Commerce アプリケーションを元の状態に戻すた `_index` に、レポートテーブルのフラッシュを検討します。 `index_price` のテーブルが最適な候補となります。 例えば、`catalog_category_product_index_storeX` テーブルの場合、X には「1」から最大ストア数までの値を含めることができます。 これらのテーブルのデータを復元するには、インデックスを再作成する必要があることに注意してください。大きなカタログの場合、インデックスの再作成に多くの時間がかかることがあります。

フラッシュしたら、wsrep 同期が完了するまで待ちます。 これで、バックアップを作成し、容量の割り当てや購入、[ 注文/請求書/出荷アーカイブ ](https://docs.magento.com/user-guide/sales/order-archive.html) 機能の有効化など、容量を追加するためにより重要な手順を実行できます。

### バイナリログ設定を確認

[!DNL MySQL] サーバーのバイナリログ設定（`log_bin` および `log_bin_index`）を確認します。 設定を有効にすると、ログファイルが大きくなる場合があります。 [ サポートチケットを作成 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) 大きなバイナリログファイルのパージをリクエストします。 また、ログが定期的にパージされ、スペースを取りすぎないように、バイナリログが正しく設定されていることを確認するようにリクエストします。

[!DNL MySQL] サーバー設定にアクセスできない場合は、サポートに問い合わせて確認してください。

### スペースの割り当てと購入

未使用のディスク領域がある場合は、[!DNL MySQL] に割り当てるディスク領域を増やします。 空きディスク容量があるかどうかを確認する方法については、[ ディスク容量制限の確認 ](/help/how-to/general/check-disk-space-limit-for-magento-commerce-cloud.md) の記事を参照してください。

* スタータープラン、すべての環境、Pro プラン統合環境では、未使用のディスク領域がある場合に割り当てることができます。 詳しくは、[ の領域の割り当て  [!DNL MySQL]](/help/how-to/general/allocate-more-space-for-mysql-in-magento-commerce-cloud.md) を参照してください。
* Pro プランのステージング環境および実稼動環境では、未使用のディスク容量がある場合に割り当てるディスク容量を増やすには、[ サポートにお問い合わせ ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) ください。

ディスク容量の上限に達してもディスク容量の不足が発生する場合は、ディスク容量の購入を検討してください。詳しくは、Adobeアカウントチームにお問い合わせください。

## 関連資料

Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
