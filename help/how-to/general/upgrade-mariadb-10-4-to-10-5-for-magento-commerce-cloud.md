---
title: クラウド上のAdobe Commerce用に MariaDB を 10.4 から 10.5 にアップグレード
description: MariaDB 10.4 は 2024 年 6 月 18 日（PT）にサポートを終了します。 この記事では、MariaDB を 10.4 から 10.5 にアップグレードして、クラウドインフラストラクチャで引き続きAdobe Commerceを使用する方法について説明します。
feature: Best Practices, Cloud
exl-id: 065840b8-28c1-4686-95fc-df3e73152845
source-git-commit: 9e218e3fadbf9941c94d309fcfb6f258d2f4faf2
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# クラウド上のAdobe Commerce用に MariaDB を 10.4 から 10.5 にアップグレード

MariaDB は、Adobe Commerceで使用されるエンタープライズオープンソースデータベースです。

MariaDB 10.4 は [2024 年 6 月 18 日（PT） &#x200B;](https://endoflife.date/mariadb) にサポート終了となります。 サポートされていないバージョンの MariaDB を使用している場合、PCI に準拠していません。 この記事では、MariaDB 10.4 から 10.5 にアップグレードして、クラウドインフラストラクチャで引き続きAdobe Commerceを使用する方法について説明します。

>[!NOTE]
>
>MariaDB 10.4 が提供終了（EOL）になると、現在のAdobe Commerce バージョンではサポートされなくなります。 すべての提供終了バージョンは、提供終了から 30 日以内に廃止することをお勧めします。

## 影響を受ける製品とバージョン

* すべてのAdobe Commerce オンプレミスおよびオンクラウドインフラストラクチャ 2.4.4 および 2.4.5

## 解決策

2024 年 6 月 11 日（PT）にリリースされる新しいセキュリティ専用パッチ（2.4.4-p9 または 2.4.5-p8）を採用して、MariaDB 10.5 との互換性を確保します。次に、以下の手順に従って MariaDB 10.4 から 10.5 にアップグレードします。

### クラウドデプロイメントのアップグレード手順

1. ECE-Tools DB backup コマンドを使用して [DB バックアップを作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/storage/snapshots) ます。 テーブル/行の更新中に問題が発生した場合は、手順 2 および 3 の前に、このバックアップを行う必要があります。
1. [&#x200B; すべてのコンパクトテーブルを確認して動的テーブルに変換する &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade)。 この手順は、データベースのアップグレード中にデータが失われる可能性を回避するために必要です。
1. MYISAM テーブルを確認します。 [&#x200B; すべての MyISAM テーブルを InnoD に変換する &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud) 必要があります。
1. データベーステーブルと行の準備（前の 2 つの手順）が完了したら、[ECE-Tools DB backup コマンドを使用して DB バックアップを作成します &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/storage/snapshots)。
1. [&#x200B; サポートチケットを開く &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) と、MariaDB 10.4 から 10.5 へのアップグレードのスケジュールを設定できます。チケットで、DB をアップグレードする日時を詳しく指定します。 サポートチームは 48 時間前に通知を受ける必要があり、マーチャントの開発チームは対応している必要があります。 アップグレードの日時について合意したら、次の手順を実行します。
   1. サイトをメンテナンスモードにして、DB アクティビティ（cron など）を停止します。
   1. ECE-Tools DB backup コマンドを使用して [DB バックアップを作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/storage/snapshots) ます。
   1. サポートチケットを使用してバックアップを完了したことをサポートに連絡します。 チケットの表示およびトラッキング手順については、サポートナレッジベースの [Adobe Commerce ヘルプセンターユーザーガイド：チケットのトラッキング &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#track-tickets) を参照してください。
   1. 次に、Adobe Commerce サポートチームは、MariaDB のアップグレードプロセスを開始します。 上記の手順がすべて実行され、データベースが平均サイズの場合、プロセスには約 1 時間かかります。 DB が大きいほど時間がかかります。 アップグレードが完了すると、チケットに関する情報が表示されます。
1. メンテナンスモードを無効にします。 開発者向けドキュメントの [&#x200B; メンテナンスモードの有効化または無効化 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。

>[!NOTE]
>
>データが失われる可能性を排除するために、アップグレード手順の前後に DB バックアップを作成することをお勧めします。 これにより、バージョンのアップグレード中に問題が発生した場合に、前の手順にロールバックできます。

## 関連資料

* オンプレミスデプロイメントの [DB アップグレードのベストプラクティスガイド &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/prepare/prerequisites)。
* [&#x200B; クラウド上のAdobe Commerce用に MariaDB 10.0 を 10.2 にアップグレード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/how-to/upgrade-mariadb-10-0-to-10-2-for-magento-commerce-cloud) する（サポートナレッジベース）。
* 開発者向けドキュメントの [0&rbrace;Adobe Commerce ライフサイクルポリシー &rbrace;。](https://experienceleague.adobe.com/ja/docs/commerce-operations/release/planning/lifecycle-policy)
