---
title: クラウド上のAdobe Commerce用に MariaDB を 10.4 から 10.5 にアップグレード
description: MariaDB 10.4 は 2024 年 6 月 18 日（PT）にサポートを終了します。 この記事では、MariaDB を 10.4 から 10.5 にアップグレードして、クラウドインフラストラクチャで引き続きAdobe Commerceを使用する方法について説明します。
feature: Best Practices, Cloud
exl-id: 065840b8-28c1-4686-95fc-df3e73152845
source-git-commit: 11f2fae3264a61413c5da1b93ef4980151a1df1e
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# クラウド上のAdobe Commerce用に MariaDB を 10.4 から 10.5 にアップグレード

MariaDB は、Adobe Commerceで使用されるエンタープライズオープンソースデータベースです。

MariaDB 10.4 はでサポート終了となります。 [2024 年 6 月 18 日（Pt）](https://endoflife.date/mariadb). サポートされていないバージョンの MariaDB を使用している場合、PCI に準拠していません。 この記事では、MariaDB 10.4 から 10.5 にアップグレードして、クラウドインフラストラクチャで引き続きAdobe Commerceを使用する方法について説明します。

>[!NOTE]
>
>MariaDB 10.4 が提供終了（EOL）になると、現在のAdobe Commerce バージョンではサポートされなくなります。 すべての提供終了バージョンは、提供終了から 30 日以内に廃止することをお勧めします。

## 影響を受ける製品とバージョン

* すべてのAdobe Commerce オンプレミスおよびオンクラウドインフラストラクチャ 2.4.4 および 2.4.5

## 解決策

2024 年 6 月 11 日（PT）にリリースされる新しいセキュリティ専用パッチ（2.4.4-p9 または 2.4.5-p8）を採用して、MariaDB 10.5 との互換性を確保します。次に、以下の手順に従って MariaDB 10.4 から 10.5 にアップグレードします。

### クラウドデプロイメントのアップグレード手順

1. を作成 [ECE-Tools DB backup コマンドを使用した DB バックアップ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots). テーブル/行の更新中に問題が発生した場合は、手順 2 および 3 の前に、このバックアップを行う必要があります。
1. [すべてのコンパクト テーブルを確認して動的テーブルに変換する](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade). この手順は、データベースのアップグレード中にデータが失われる可能性を回避するために必要です。
1. MYISAM テーブルを確認します。 次の操作が必要です [すべての MyISAM テーブルを InnoD に変換する](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud).
1. データベーステーブルと行の準備（前の 2 つの手順）が完了したら、 [ECE-Tools DB backup コマンドを使用した DB バックアップ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots).
1. [サポートチケットを開く](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) mariaDB 10.4 から 10.5 へのアップグレードをスケジュールします。チケットで、DB をアップグレードする日時を詳しく指定します。 サポートチームは 48 時間前に通知を受ける必要があり、マーチャントの開発チームは対応している必要があります。 アップグレードの日時について合意したら、次の手順を実行します。
   1. サイトをメンテナンスモードにして、DB アクティビティ（cron など）を停止します。
   1. を作成 [ECE-Tools DB backup コマンドを使用した DB バックアップ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots).
   1. サポートチケットを使用してバックアップを完了したことをサポートに連絡します。 チケットを表示および追跡する手順については、を参照してください。 [Adobe Commerce ヘルプセンターユーザーガイド：チケットの追跡](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) サポートナレッジベースで。
   1. 次に、Adobe Commerce サポートチームは、MariaDB のアップグレードプロセスを開始します。 上記の手順がすべて実行され、データベースが平均サイズの場合、プロセスには約 1 時間かかります。 DB が大きいほど時間がかかります。 アップグレードが完了すると、チケットに関する情報が表示されます。
1. メンテナンスモードを無効にします。 こちらを参照してください [メンテナンスモードの有効化または無効化](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) 開発者向けドキュメントを参照してください。

>[!NOTE]
>
>データが失われる可能性を排除するために、アップグレード手順の前後に DB バックアップを作成することをお勧めします。 これにより、バージョンのアップグレード中に問題が発生した場合に、前の手順にロールバックできます。

## 関連資料

* [DB アップグレードのベストプラクティスガイド](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/prerequisites) オンプレミスのデプロイメントの場合。
* [クラウド上のAdobe Commerce用に MariaDB を 10.0 から 10.2 にアップグレード](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/upgrade-mariadb-10-0-to-10-2-for-magento-commerce-cloud) サポートナレッジベースで。
* [Adobe Commerce ライフサイクルポリシー](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/lifecycle-policy) 開発者向けドキュメントを参照してください。
