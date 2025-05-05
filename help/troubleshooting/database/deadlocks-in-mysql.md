---
title: MySQL のデッドロック
description: この文書では、MySQL のデッドロックについて説明し、サイトのダウン、データベースの読み込み停止、またはその他のAdobe Commerceの問題が発生した場合に、デッドロックを特定して解決できるようにします。
exl-id: 529d1c0b-77f3-4604-9878-e7ea2c9c3640
feature: Best Practices, Services
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# MySQL のデッドロック

この文書では、MySQL のデッドロックについて説明し、サイトのダウン、データベースの読み込み停止、またはその他のAdobe Commerceの問題が発生した場合に、デッドロックを特定して解決できるようにします。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.2.x および 2.3.x
* クラウドインフラストラクチャー 2.2.x および 2.3.x 上のAdobe Commerce

## 問題

MySQL のデッドロックは、2 つ以上のトランザクションが相互に保持してロックを要求する場合に発生します。 デッドロックが存在する場合、必ずしも問題を示しているわけではありませんが、多くの場合、発生した他の MySQL またはAdobe Commerceの問題の症状です。

多くの場合、アプリケーション、デプロイメントまたは MySQL ログで、「*&quot;deadlock&quot;* エラーまたは *&quot;ロックを取得しようとしたときにデッドロックが見つかりました。トランザクションを再開してみてください。&quot;* が表示されます。

## 原因：

デッドロックには複数の原因がありますが、最も一般的な原因は、DML/DDL クエリを同時に実行しながら、何らかのインタラクション（web サイト/プロセス/cron ジョブ/その他のユーザー/MySQL メンテナンス/MySQL インポート）を実行することです。

例えば、MySQL データベースインポートが停止するのを避けるためには、まずサイトをメンテナンスモードにして、デッドロックや停止したデータベースインポートの原因となる可能性のある SQL リクエストをデータベースに受け取らないようにすることがベストプラクティスです。

## 解決策

1. アプリケーション、デプロイメント、または MySQL ログでデッドロックエラーを確認します。
   * [Adobe CommerceとMagento Open Sourceログの場所 ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/enable-logging.html?lang=ja)
   * [ クラウドインフラストラクチャログ上のAdobe Commerceの場所 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=ja)
1. コマンド `mysql -e 'show full processlist';` を使用して、MySQL プロセスのリストでプロセスが実行されているかどうかを確認します。
1. クラウドインフラストラクチャー上のAdobe Commerceで、MySQL スレーブが有効になっていることを確認します。 詳しくは、「[ 変数をデプロイ（MYSQL\_USE\_SLAVE\_CONNECTION） ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html?lang=ja#mysql_use_slave_connection)」を参照してください。
1. 関連するエラーに応じて、ソリューション自体が表示されるか、[ サポートチケット ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) を開く必要がある場合は、役立つログ情報を含める必要がある場合があります。

## 関連資料

* [ デッドロックを最小限に抑えて処理する方法 ](https://dev.mysql.com/doc/refman/5.7/en/innodb-deadlocks-handling.html)
* [ インデクサーの最適化 – インデクサーテーブルの切り替え ](https://developer.adobe.com/commerce/php/development/components/indexing/optimization/)
* [ 一括操作 – メッセージの使用 ](https://developer.adobe.com/commerce/php/development/components/message-queues/bulk-operations/)

>[!NOTE]
>
>この記事には、人種差別的、性差別的、または抑圧的と思われる業界標準のソフトウェア用語が依然として含まれており、読者が苦痛を感じたり、トラウマを抱いたり、歓迎されないと感じたりする場合があることを認識しています。 Adobeでは、これらの用語をアドビのコード、ドキュメントおよびユーザーエクスペリエンスから削除するよう取り組んでいます。
