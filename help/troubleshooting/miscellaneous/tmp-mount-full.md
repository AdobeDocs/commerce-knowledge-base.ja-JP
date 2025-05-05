---
title: Adobe Commerceの/tmp mount full のトラブルシューティング
description: この記事では、'/tmp' マウントがいっぱいになり、サイトがダウンして、ノードに SSH 接続できない場合の解決策を示します。
exl-id: e72d0f99-0060-474b-bb1c-2851896e1e43
feature: Storage
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Adobe Commerceの/tmp mount full のトラブルシューティング

この記事では、`/tmp` マウントがいっぱいになり、サイトがダウンして、ノードに SSH 接続できない場合の解決策を示します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.3.0 ～ 2.3.6-p1、2.4.0 ～ 2.4.2

## 問題

`/tmp` マウントがいっぱいになると、次のエラーなど、様々な症状が発生する可能性があります。

* *SQLSTATE[HY000]：一般エラー：3 ファイルの書き込み中にエラーが発生しました*
* *エラーコード：28*
* *デバイスの空き領域がありません（28）*
* *エラー：session_start （）：失敗：デバイスに空き領域がありません*
* *エラー 1 （HY000）: ファイル &#39;/tmp/* を作成/書き込めません
* *SQL エラー：3、SQLState: HY000*
* *一般的なエラー：1021 ディスクがいっぱいです（/tmp）*
* *SSH 経由でノードにアクセスできない：*
  *bash:here-document の一時ファイルを作成できません：デバイスにスペースが残っていません*
* *errno: 28 「デバイスにスペースが残っていません」*
* *mysqld: ディスクの書き込みが完了しています&#39;/tmp&#39;*
* *[エラー ] mysqld: ディスクがいっぱいです（/tmp）*
* *SQLSTATE[HY000]：一般的なエラー：1 ファイル &#39;/tmp/&#39;を作成/書き込めません*
* *SQLSTATE[HY000]：一般的なエラー：ファイル &#39;/tmp/&#39;を開いているときに 23 リソース不足*
* *エラーコード：24 「開いているファイルが多すぎます」*
* *エラーを取得：23 : ファイルを開く際にリソースが不足しています*


<u> 再現手順：</u>

`/tmp` マウントのフル状態を確認するには、CLI スイッチで `/tmp` に切り替え、次のコマンドを実行します。

```bash
 df -h
```

<u> 期待される結果 </u>:

80% 未満。

<u> 実際の結果 </u>:

約 100%。

## 原因：

`/tmp` マウントのファイルが多すぎます。次の原因が考えられます：

* 無効な SQL クエリで大きな一時テーブルや多すぎる一時テーブルが生成されています。
* `/tmp` ディレクトリに書き込むサービス。
* `/tmp` ディレクトリに残っているデータベースのバックアップ/ダンプ。

## 解決策

ある程度のスペースを解放するためにできることと、`\tmp` ーザーがいっぱいになるのを防ぐベストプラクティスがあります。

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

Use% が 70% 未満であることを確認します。 inode はファイルと相関関係があります。 パーティションからファイルを削除すると、inode が解放されます。

### ストレージスペースの確認と解放

`/tmp` にファイルを保存するサービスがいくつかあります。

#### MySQL の容量を確認して解放する

サポートナレッジベースの [ クラウドインフラストラクチャ上のAdobe Commerceで MySQL のディスク容量が少ない > ストレージ容量を確認して解放する ](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md#check_and_free) の手順に従います。

#### Elasticsearchのヒープダンプをチェック

>[!WARNING]
>
>ヒープダンプには、問題の調査に役立つ可能性のあるログ情報が含まれています。 10 日以上、別の場所に保存することを検討してください。

システムシェルを使用して heapdumps （`*.hprof`）を削除します。

```bash
find /tmp/*.hprof -type f -delete
```

別のユーザー（この場合はElasticsearch）が作成したファイルを削除する権限を持っていないが、ファイルが大きいことがわかっている場合は、[ サポートチケットを作成 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) して対処してください。

#### データベースのダンプ/バックアップのチェック

>[!WARNING]
>
>データベースのバックアップは通常、目的のために作成されます。 それでもファイルが必要かどうか不明な場合は、ファイルを削除する代わりに、別の場所に移動することを検討してください。

`.sql` ファイルまたは `.sql.gz` ファイルの `/tmp` を確認してクリーンアップします。 これらは、バックアップ時に ece-tools によって作成されたり、`mysqldump` ツールを使用して手動でデータベースダンプを作成したりするときに作成されることがあります。

### ベストプラクティス

`/tmp` がいっぱいの問題を回避するには、次の推奨事項に従います。

* 検索に MySQL を使用しないでください。 検索のElasticsearchにより、通常、重い一時テーブルの作成のほとんどが不要になります。 開発者向けドキュメントの [Elasticsearchを使用するためのAdobe Commerceの設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/search/configure-search-engine) を参照してください。
* インデックスのない列に対して `SELECT` クエリを実行しないでください。このクエリは大量の一時ディスク領域を消費します。 インデックスを追加することもできます。
* CLI で次のコマンドを実行して、`/tmp` をクリーンアップする cron を作成します。

  ```bash
  sudo find /tmp -type f -atime +10 -delete
  ```

## 関連資料

[ クラウドインフラストラクチャ上のAdobe Commerceで MySQL のディスク容量が少ない ](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md) というアドビのサポートナレッジベースを参照してください。
