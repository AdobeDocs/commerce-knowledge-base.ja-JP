---
title: 環境の再配置に失敗したか、MySQL サーバーが使用されなくなりました
description: この記事では、MySQL に割り当てられた領域が停止してデプロイメントが停止したり、データベース接続エラーが発生したりするAdobe Commerce（すべてのデプロイメント方法）の問題に対する解決策を提供します。
exl-id: 2086b45a-0bfe-45cc-bef9-1b6f09ddb70a
feature: Deploy, Services
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# 環境の再配置に失敗したか、MySQL サーバーが使用されなくなりました

この記事では、MySQL に割り当てられた領域が停止してデプロイメントが停止したり、データベース接続エラーが発生したりするAdobe Commerce（すべてのデプロイメント方法）の問題に対する解決策を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure （すべてのバージョン）

## 問題

* デプロイプロセスが失敗し、デプロイログ（コマンドラインと UI ログ）に次のエラーが記録されます。```bash    Re-deploying environment abcdefghijklm-master-7rqtwti         E: Environment redeployment failed    ```
* Adobe Commerceが 503 エラーで応答し、次のエラーメッセージがアプリケーションログに表示されます。    ```bash    SQLSTATE[HY000] [2006] MySQL server has gone away    ```    MySQL サーバーに接続すると、次のエラーが表示されます。    ```bash    ERROR 2013 (HY000): Lost connection to MySQL server at 'reading initial communication packet', system error: 0 "Internal error/check (Not system error)"    ```

## 原因：

この問題の最も考えられる原因は、MySQL データベースの割り当て領域が低すぎることです。 この場合に該当することを確認するには、後で説明するように、MySQL で使用可能な領域を確認します。

### MySQL に十分な容量があるかどうかを確認します

クラウドインフラストラクチャー上のすべてのAdobe Commerce スタータープランアーキテクチャ環境、およびクラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャの [ 統合環境 ](/help/announcements/adobe-commerce-announcements/integration-environment-enhancement-request-pro-and-starter.md) の場合は、環境に [SSH](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html) で次のコマンドを実行します。

```bash
magento-cloud db:size
```

Pro アーキテクチャのステージング環境または実稼動環境の場合は、[ 環境に SSH 接続 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html) し、`df -h` を実行します   `| grep mysql` コマンド。 結果は次のようになります。

```bash
sxpe7gigd5ok2@i-00baa9e24f31dba41:~$ df -h | grep mysql
/dev/xvdj                            40G  7.4G   32G  19% /data/mysql
```

## 解決策

### この問題を解決するには、MySQL 用により多くの領域を割り当てる必要があります。

すべての Starter アーキテクチャおよび Pro アーキテクチャ統合環境では、`mysql: disk:` パラメーターを増やして `.magento/services.yaml` ファイルで行います。 例：

```yaml
mysql:
    type: mysql:10.0
    disk: 2048
```

詳しくは、[MySQL サービスの設定 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/mysql.html) の記事を参照してください。

Pro アーキテクチャのステージング環境または実稼動環境用にこれらの変更を行うには、[ サポートチケット ](https://support.magento.com) を作成する必要があります。 ただし、通常は、Adobe Commerceがこれらのパラメーターをモニタリングし、アラートを送信したり、契約に従ってアクションを実行したりするので、Pro アーキテクチャのステージング/実稼動で対処する必要はありません。

### 変更の適用

`.magento/services.yaml` ファイルを変更したら、変更を適用するために、コミットしてプッシュする必要があります。 プッシュはデプロイメントプロセスをトリガーします。
