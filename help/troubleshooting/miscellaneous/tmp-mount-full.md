---
title: Adobe Commerceの/tmp mount full のトラブルシューティング
description: この記事では、'/tmp' マウントがいっぱいになり、サイトがダウンして、ノードに SSH 接続できない場合の解決策を示します。
exl-id: e72d0f99-0060-474b-bb1c-2851896e1e43
feature: Storage
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Adobe Commerceの/tmp mount full のトラブルシューティング

この記事では、次のような場合の解決策を提供します `/tmp` マウントがいっぱいです。サイトがダウンしている可能性があり、ノードに SSH 接続できません。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.3.0 ～ 2.3.6-p1、2.4.0 ～ 2.4.2

## 問題

この `/tmp` マウントがいっぱいになると、次のエラーなど、様々な症状が発生する可能性があります。

* *SQLSTATE[000 HY]：一般エラー：3 ファイルの書き込み中にエラーが発生しました*
* *エラーコード：28*
* *デバイスにスペースが残っていません（28）*
* *エラー：session_start （）：失敗：デバイスに空き領域がありません*
* *エラー 1 （HY000）: ファイル &#39;/tmp/を作成/書き込めません*
* *SQL エラー：3、SQLState: HY000*
* *一般的なエラー：1021 ディスクがいっぱいです（/tmp）*
* *SSH 経由でノードにアクセスできません：*
  *bash: here-document の一時ファイルを作成できません：デバイスにスペースが残っていません*
* *errno:28 「デバイスにスペースが残っていない」*
* *mysqld : ディスクが「/tmp」を完全に書き込んでいます*
* *[エラー] mysqld: ディスクがいっぱいです（/tmp）*
* *SQLSTATE[000 HY]：一般的なエラー：1 ファイル「/tmp/」を作成/書き込めません*
* *SQLSTATE[000 HY]：一般エラー：「/tmp/」ファイルを開いたときに 23 個のリソースが不足しています*
* *エラーコード：24 「開いているファイルが多すぎます」*
* *エラーを取得しました：23 : ファイルを開く際にリソースが不足しています*


<u>再現手順：</u>

がどのくらいいっぱいかを確認するには `/tmp` マウントは、CLI スイッチで次のように指定します `/tmp` さらに、次のコマンドを実行します。

```bash
 df -h
```

<u>期待される結果</u>:

80% 未満。

<u>実際の結果</u>:

約 100%。

## 原因：

この `/tmp` マウントしたファイルが多すぎます。次の原因が考えられます：

* 無効な SQL クエリで大きな一時テーブルや多すぎる一時テーブルが生成されています。
* に書き込むサービス `/tmp` ディレクトリ。
* に残っているデータベースのバックアップ/ダンプ `/tmp` ディレクトリ。

## 解決策

ある程度のスペースを解放するために実行できることと、それを妨げるベストプラクティスがあります `\tmp` 満腹から。

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

にファイルを保存しているいくつかのサービスがあります `/tmp`.

#### MySQL の容量を確認して解放する

の指示に従います。 [クラウドインフラストラクチャー上のAdobe Commerceで MySQL のディスク領域が不足しています > ストレージ領域を確認して解放してください](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md#check_and_free) サポートナレッジベースで。

#### Elasticsearchのヒープダンプをチェック

>[!WARNING]
>
>ヒープダンプには、問題の調査に役立つ可能性のあるログ情報が含まれています。 10 日以上、別の場所に保存することを検討してください。

ヒープダンプを削除します（`*.hprof`）を使用します。

```bash
find /tmp/*.hprof -type f -delete
```

別のユーザー（この場合はElasticsearch）が作成したファイルを削除する権限を持っていないが、ファイルが大きい場合は、 [サポートチケットを作成](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) それらに対処するために。

#### データベースのダンプ/バックアップのチェック

>[!WARNING]
>
>データベースのバックアップは通常、目的のために作成されます。 それでもファイルが必要かどうか不明な場合は、ファイルを削除する代わりに、別の場所に移動することを検討してください。

チェック `/tmp` （用） `.sql` または `.sql.gz` ファイルと、それらをクリーンアップします。 これらは、バックアップ時に ece-tools によって作成されたり、を使用して手動でデータベースダンプを作成したりするときに作成されることがあります `mysqldump` ツール。

### ベストプラクティス

に関する問題の発生を回避するには `/tmp` いっぱいの場合は、次の推奨事項に従います。

* 検索に MySQL を使用しないでください。 検索のElasticsearchにより、通常、重い一時テーブルの作成のほとんどが不要になります。 参照： [Elasticsearchを使用するようにAdobe Commerceを設定する](https://devdocs.magento.com/guides/v2.2/config-guide/elasticsearch/configure-magento.html) 開発者向けドキュメントを参照してください。
* を実行しないでください。 `SELECT` インデックスのないカラムに対してクエリを実行すると、大量の一時ディスク領域が消費されます。 インデックスを追加することもできます。
* クリーンアップする cron を作成 `/tmp` CLI で次のコマンドを実行します。

  ```bash
  sudo find /tmp -type f -atime +10 -delete
  ```

## 関連資料

[クラウドインフラストラクチャー上のAdobe Commerceで MySQL のディスク領域が不足している](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md) サポートナレッジベースで。
