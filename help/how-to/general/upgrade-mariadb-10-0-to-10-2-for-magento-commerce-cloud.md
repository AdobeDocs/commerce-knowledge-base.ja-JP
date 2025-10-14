---
title: クラウド上のAdobe Commerce用に MariaDB を 10.0 から 10.2 にアップグレード
description: MariaDB 10.0 と 10.1 は提供終了（EOL）となります。 [ サポートは、2019 年 3 月 31 日に終了し、2020 年 10 月 17 日に終了しました ] （https://endoflife.date/mariadb）。 この記事では、クラウドインフラストラクチャー上でAdobe Commerceを使用するために、MariaDB を 10.0 から 10.2 または 10.2 から 10.3 または 10.4 にアップグレードする方法について説明します。
exl-id: bf66798b-f05c-482f-a2b4-b9bef92b0bab
feature: Best Practices, Cloud
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# クラウド上のAdobe Commerce用に MariaDB を 10.0 から 10.2 にアップグレード

MariaDB 10.0 と 10.1 は提供終了（EOL）となります。 [&#x200B; サポートは、2019 年 3 月 31 日に終了し、2020 年 10 月 17 日に終了しました &#x200B;](https://endoflife.date/mariadb)。 この記事では、クラウドインフラストラクチャー上でAdobe Commerceを使用するために、MariaDB を 10.0 から 10.2 または 10.2 から 10.3 または 10.4 にアップグレードする方法について説明します。

>[!NOTE]
>
>MariaDB 10.0 は提供終了（EOL）となり、現在のAdobe Commerce バージョンではサポートされていません。 すべての提供終了バージョンは、提供終了から 30 日以内に廃止することをお勧めします。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.3.x 上のAdobe Commerceには MariaDB 10.2 をお勧めします。
* 2.4.x には MariaDB 10.4 をお勧めします。MariaDB 10.3 は、クラウドインフラストラクチャー 2.4.x 上のAdobe Commerceとも互換性があります。

## アップグレード手順

MariaDB 10.0 から 10.2 または 10.2 から 10.3 または 10.4 にアップグレードするには、次の手順を実行します。

1. ECE-Tools DB backup コマンドを使用して [DB バックアップを作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/storage/snapshots) ます。 テーブル/行の更新中に問題が発生した場合に備えて、手順 2 および 3 の前にこれを行う必要があります。
1. [&#x200B; すべてのコンパクトテーブルを確認して動的テーブルに変換する &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html?lang=ja)。 これは、データベースのアップグレード中にデータが失われる可能性を回避するために必要です。
1. MYISAM テーブルを確認します。 [&#x200B; すべての MyISAM テーブルを InnoD に変換する &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html?lang=ja) 必要があります。
1. データベーステーブルと行の準備（前の 2 つの手順）が完了したら、[ECE-Tools DB backup コマンドを使用して DB バックアップを作成します &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/storage/snapshots)。
1. [&#x200B; サポートチケットを開く &#x200B;](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) と、MariaDB 10.0 から 10.2 または 10.2 から 10.3 または 10.4 へのアップグレードのスケジュールが設定されます。チケットの詳細で、DB をアップグレードする日時を指定します。 サポートチームには 48 時間前の通知が必要で、マーチャント開発チームを使用できる必要があります。 アップグレードの日時について合意したら、次の手順を実行します。
   1. サイトをメンテナンスモードにして、DB アクティビティ（cron など）を停止します。
   1. ECE-Tools DB backup コマンドを使用して [DB バックアップを作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/storage/snapshots) ます。
   1. バックアップが完了したことをサポートに連絡します。 これを行うには、サポートチケットを使用します。 チケットの表示およびトラッキング手順については、サポートナレッジベースの [Adobe Commerce ヘルプセンターユーザーガイド：チケットのトラッキング &#x200B;](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) を参照してください。
   1. Adobe Commerce サポートチームが MariaDB のアップグレードプロセスを開始します。 上記の手順をすべて実行し、データベースが平均サイズの場合は、約 1 時間で完了します。 DB が大きいと、時間がかかります。 アップグレードが完了すると、チケットを通じて通知されます。
1. メンテナンスモードを無効にします。 開発者向けドキュメントの [&#x200B; メンテナンスモードの有効化または無効化 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。

## 関連資料

Adobe Commerce 2.4.x の要件について詳しくは、開発者向けドキュメントの [Adobe Commerce 2.4 の必要システム構成/データベース &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/system-requirements#database) を参照してください。
