---
title: Adobe Commerce クラウド版のMariaDB 10.4から10.5へのアップグレード
description: MariaDB 10.4は2024年6月18日にサポート終了となります。 この記事では、Adobe Commerce on cloud infrastructureを引き続き使用するために、MariaDBを10.4から10.5にアップグレードする方法について説明します。
feature: Best Practices, Cloud
exl-id: 065840b8-28c1-4686-95fc-df3e73152845
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%
---
# Adobe Commerce クラウド版のMariaDB 10.4から10.5へのアップグレード

MariaDBは、Adobe Commerceで使用されるエンタープライズオープンソースデータベースです。

MariaDB 10.4は、[2024年6月18日](https://endoflife.date/mariadb)にサポート終了に達しました。 サポートされていないバージョンのMariaDBを使用している場合、PCIに準拠しなくなりました。 この記事では、Adobe Commerce on cloud infrastructureを引き続き使用するために、MariaDB 10.4から10.5にアップグレードする方法について説明します。

>[!NOTE]
>
>MariaDB 10.4が提供終了（EOL）に達すると、現在のAdobe Commerce版ではサポートされなくなります。 EOLから30日以内にEOL バージョンを削除することをお勧めします。

## 影響を受ける製品とバージョン

* すべてのAdobe Commerce オンプレミスおよびクラウドインフラストラクチャ 2.4.4および2.4.5

## Solution

MariaDB 10.5との互換性を確保するために、2024年6月11日にリリースされる新しいセキュリティ専用パッチ（2.4.4-p9または2.4.5-p8）を採用します。 次に、以下の手順に従って、MariaDB 10.4から10.5にアップグレードします。

### クラウド デプロイメントのアップグレード手順

1. ECE-Tools DB backup コマンド ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots)を使用して[DB バックアップを作成します。 このバックアップは、テーブル/行の更新中に何か問題が発生した場合に備えて、手順2と3の前に実行する必要があります。
1. [すべてのコンパクト テーブルをチェックして動的テーブルに変換します](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade)。 この手順は、データベースのアップグレード中にデータが失われる可能性を回避するために必要です。
1. MYISAM テーブルを確認します。 すべてのMyISAM テーブルを[InnoD](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud)に変換する必要があります。
1. データベースのテーブルと行（前の2つの手順）を準備したら、ECE-Tools DB バックアップ コマンド ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots)を使用して[DB バックアップを作成します。
1. [ サポートチケット ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を開いて、MariaDB 10.4から10.5へのアップグレードをスケジュールします。 チケットで、DBをアップグレードする日時を詳細に指定します。 サポートチームには48時間前の通知が必要であり、マーチャントの開発チームには連絡できる必要があります。 アップグレードの日時を決定したら、次の操作を行います。
   1. サイトをメンテナンスモードにし、cronsなどのDB アクティビティを停止します。
   1. ECE-Tools DB backup コマンド ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots)を使用して[DB バックアップを作成します。
   1. サポートチケットを使用してバックアップが完了したことをサポートにお知らせください。 チケットの表示とトラッキングの手順については、サポートナレッジベースの「[Adobe Commerce ヘルプセンターのユーザーガイド：チケットのトラッキング ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#track-tickets)」を参照してください。
   1. その後、Adobe Commerce サポートチームはMariaDB アップグレードプロセスを開始します。 上記のすべての手順が実行され、データベースが平均サイズの場合、プロセスには約1時間かかります。 DBが大きいほど時間がかかります。 アップグレードが完了すると、チケットを通じて通知されます。
1. メンテナンスモードを無効にします。 開発者ドキュメントの[ メンテナンスモードを有効または無効にする](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode)を参照してください。

>[!NOTE]
>
>データ損失の可能性を排除するために、アップグレード手順の前後にDB バックアップを作成することをお勧めします。 これにより、バージョンのアップグレード中に問題が発生した場合は、前の手順にロールバックできます。

## 関連トピックス

* オンプレミスのデプロイメントに関する[DB アップグレードのベストプラクティス ガイド ](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/prerequisites)。
* [MariaDBのアップグレードの前提条件：実装プレイブックのアップグレード ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade#prepare-your-database-for-the-upgrade)用にデータベースを準備します。
* 開発者向けドキュメントの[Adobe Commerce ライフサイクルポリシー](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/lifecycle-policy)を参照してください。
