---
title: 同じ期間に複数の cron ジョブがスケジュールされました
description: この記事では、特定のタスクの変数がAdobe Commerce管理者で編集された後、複数の cron ジョブを同時に実行するようにスケジュールする問題に関連する、既知のCommerce 2.2.2 問題のパッチを提供します。
exl-id: a3c1fe77-ed4c-43b5-8d6f-e5c549096c73
feature: Cache
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---

# 同じ期間に複数の cron ジョブがスケジュールされました

この記事では、特定のタスクの変数がAdobe Commerce管理者で編集された後、複数の cron ジョブを同時に実行するようにスケジュールする問題に関連する、既知のCommerce 2.2.2 問題のパッチを提供します。

## 問題

Cron が 1 分ごとに実行されるように設定されている場合、管理で 3 つのスケジュールされたタスクの時間変数を編集すると、 `cron_schedule` データベース テーブルには、同時に実行するようにスケジュールされた複数のタスクのグループが表示されます。

<u>再現手順</u>:

1. Commerce Admin で、に移動します。 **ストア** > 設定 > **設定** > **詳細** > **システム** > **Cron （スケジュールされたタスク）** > **グループの Cron 設定オプション : デフォルト。**
1. 次のオプションを設定します。
   * **履歴クリーンアップ間隔**：をクリアします **システムを使用** チェックボックス、に設定 *1440*.
   * **成功履歴の有効期間**：をクリアします **システムを使用** チェックボックス、に設定 *1440*.
   * **失敗履歴の有効期間**：をクリアします **システムを使用** チェックボックス、に設定 *1440*.

1. クリック **設定を保存**.
1. SSH で、 `crontab -e` コマンド。
1. cron を毎分実行するように設定します。
1. 3 つのターミナルタブ/ウィンドウを開きます。
1. Adobe Commerceに移動 `root/base/project` 各ターミナルウィンドウのディレクトリ。
1. 各タブ/ウィンドウで次のコマンドを実行します。

   ```bash
   bin/magento cache:flush && bin/magento cron:run && bin/magento cache:flush && bin/magento cron:run
   ```

1. MySQL に移動し、次のクエリを実行します。

   ```sql
   SELECT job_code, scheduled_at, count as count FROM cron_schedule GROUP BY job_code, scheduled_at HAVING count > 1 ORDER BY scheduled_at;
   ```

1. 同時に実行するようにスケジュールされたタスクのグループを参照してください。

<u>期待される結果</u>:1 つの cron `job_code` は、特定の期間にスケジュールされる必要があります。

<u>実際の結果</u>：同じ期間に対してスケジュールされた cron ジョブが複数あります。

## 解決策

クラウドインフラストラクチャー上のAdobe Commerceのマーチャントの場合、 [ece-tools の更新](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package.html) が問題を解決します。

Adobe Commerce オンプレミスのマーチャントは、問題を解決するために、接続されたパッチの 1 つを適用する必要があります。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後までスクロールしてファイル名をクリックするか、次のリンクのいずれかをクリックします。

* [MDVA-11304\_EE\_2.1.4\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.1.4_COMPOSER_v1.patch.zip)
* [MDVA-11304\_EE\_2.1.5\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.1.5_COMPOSER_v1.patch.zip)
* [MDVA-11304\_EE\_2.1.13\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.1.13_COMPOSER_v1.patch.zip)
* [MDVA-11304\_EE\_2.1.14\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.1.14_COMPOSER_v1.patch.zip)
* [MDVA-11304\_EE\_2.2.0\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.2.0_COMPOSER_v1.patch.zip)
* [MDVA-11304\_EE\_2.2.2\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.2.2_COMPOSER_v1.patch.zip)
* [MDVA-11304\_EE\_2.2.4\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.2.4_COMPOSER_v1.patch.zip)

### 互換性のあるAdobe Commerce バージョン

パッチは、パッチ ファイル名に示されている特定のバージョンに対して作成されました。 例えば、MDVA-11304\_EE\_2.2.4\_COMPOSER\_v1.patch はAdobe Commerce 2.2.4 用に作成されたもので、このバージョンで使用するのに最適なパッチです。

パッチは、次のバージョンとも互換性があります。

* Adobe Commerce オンプレミス 2.1.0～2.1.4 の場合： [MDVA-11304\_EE\_2.1.4\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.1.4_COMPOSER_v1.patch.zip) このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー上のAdobe Commerce 2.1.0～2.1.4
* Adobe Commerce オンプレミス 2.1.5～2.1.12 の場合： [MDVA-11304\_EE\_2.1.5\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.1.5_COMPOSER_v1.patch.zip) このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー上のAdobe Commerce 2.1.5-2.1.12
* クラウドインフラストラクチャー 2.1.13 上のAdobe Commerceの場合： [MDVA-11304\_EE\_2.1.13\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.1.13_COMPOSER_v1.patch.zip)
* Adobe Commerce オンプレミス 2.1.14-2.1.17 の場合： [MDVA-11304\_EE\_2.1.14\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.1.14_COMPOSER_v1.patch.zip) このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * Adobe Commerce オンプレミス 2.1.18
   * クラウドインフラストラクチャー上のAdobe Commerce 2.1.14-2.1.18
* Adobe Commerce オンプレミス 2.2.0～2.2.1 の場合： [MDVA-11304\_EE\_2.2.0\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.2.0_COMPOSER_v1.patch.zip) このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー上のAdobe Commerce 2.2.0-2.2.1
* Adobe Commerce オンプレミス 2.2.0～2.2.3 の場合： [MDVA-11304\_EE\_2.2.2\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.2.2_COMPOSER_v1.patch.zip) このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー上のAdobe Commerce 2.2.0-2.2.3
* Adobe Commerce オンプレミス 2.2.4 の場合： [MDVA-11304\_EE\_2.2.4\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-11304_EE_2.2.4_COMPOSER_v1.patch.zip) このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー 2.2.4 上のAdobe Commerce

## パッチの適用方法

参照： [Adobe Commerceが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで、の手順を確認します。

## 添付ファイル
