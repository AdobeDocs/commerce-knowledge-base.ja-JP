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

毎分実行するように cron が設定されている場合、Admin で 3 つのスケジュールされたタスクの時間変数を編集すると、`cron_schedule` のデータベーステーブルには、同時に実行するようにスケジュールされた複数のタスクのグループが表示されます。

<u> 再現手順 </u>:

1. Commerce管理で、**ストア**/設定/**設定**/**詳細**/**システム**/**Cron （スケジュールされたタスク）**/**グループの Cron 設定オプション：デフォルト** に移動します。
1. 次のオプションを設定します。
   * **履歴クリーンアップ間隔**: **システムを使用** チェックボックスをオフにして、*1440* に設定します。
   * **成功履歴の有効期間**:「**システムを使用**」チェックボックスをオフにして、「*1440*」に設定します。
   * **エラー履歴の有効期間**:「**システムを使用**」チェックボックスをオフにして、「*1440*」に設定します。

1. 「**設定を保存**」をクリックします。
1. SSH で `crontab -e` コマンドを実行します。
1. cron を毎分実行するように設定します。
1. 3 つのターミナルタブ/ウィンドウを開きます。
1. 各ターミナルウィンドウのAdobe Commerce `root/base/project` ディレクトリに移動します。
1. 各タブ/ウィンドウで次のコマンドを実行します。

   ```bash
   bin/magento cache:flush && bin/magento cron:run && bin/magento cache:flush && bin/magento cron:run
   ```

1. MySQL に移動し、次のクエリを実行します。

   ```sql
   SELECT job_code, scheduled_at, count as count FROM cron_schedule GROUP BY job_code, scheduled_at HAVING count > 1 ORDER BY scheduled_at;
   ```

1. 同時に実行するようにスケジュールされたタスクのグループを参照してください。

<u> 期待される結果 </u>：特定の期間に 1 つの Cron `job_code` をスケジュールする必要があります。

<u> 実際の結果 </u>：同じ期間に対してスケジュールされた複数の Cron ジョブがあります。

## 解決策

クラウドインフラストラクチャー上のAdobe Commerceのマーチャントの場合、[ECE ツールを更新する ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package.html) ことで問題が解決します。

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

* Adobe Commerce オンプレミス 2.1.0～2.1.4 の場合：[MDVA-11304\_EE\_2.1.4\_COMPOSER\_v1.patch をダウンロードします ](assets/MDVA-11304_EE_2.1.4_COMPOSER_v1.patch.zip) このパッチは、次のAdobe Commerce バージョンおよびエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー上のAdobe Commerce 2.1.0～2.1.4
* Adobe Commerce オンプレミス 2.1.5-2.1.12 の場合：[MDVA-11304\_EE\_2.1.5\_COMPOSER\_v1.patch をダウンロードし ](assets/MDVA-11304_EE_2.1.5_COMPOSER_v1.patch.zip) す。このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー上のAdobe Commerce 2.1.5-2.1.12
* Cloud Infrastructure 2.1.13 でのAdobe Commerceの場合：[MDVA-11304\_EE\_2.1.13\_COMPOSER\_v1.patch をダウンロードします ](assets/MDVA-11304_EE_2.1.13_COMPOSER_v1.patch.zip)
* Adobe Commerce オンプレミス 2.1.14-2.1.17 の場合：[MDVA-11304\_EE\_2.1.14\_COMPOSER\_v1.patch をダウンロード ](assets/MDVA-11304_EE_2.1.14_COMPOSER_v1.patch.zip) ます。このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * Adobe Commerce オンプレミス 2.1.18
   * クラウドインフラストラクチャー上のAdobe Commerce 2.1.14-2.1.18
* Adobe Commerce オンプレミス 2.2.0-2.2.1 の場合：[MDVA-11304\_EE\_2.2.0\_COMPOSER\_v1.patch をダウンロード ](assets/MDVA-11304_EE_2.2.0_COMPOSER_v1.patch.zip) ます。このパッチは、次のAdobe Commerce バージョンおよびエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー上のAdobe Commerce 2.2.0-2.2.1
* Adobe Commerce オンプレミス 2.2.0～2.2.3 の場合：[MDVA-11304\_EE\_2.2.2\_COMPOSER\_v1.patch をダウンロード ](assets/MDVA-11304_EE_2.2.2_COMPOSER_v1.patch.zip) ます。このパッチは、次のAdobe Commerce バージョンおよびエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー上のAdobe Commerce 2.2.0-2.2.3
* Adobe Commerce オンプレミス 2.2.4 の場合：[MDVA-11304\_EE\_2.2.4\_COMPOSER\_v1.patch をダウンロードし ](assets/MDVA-11304_EE_2.2.4_COMPOSER_v1.patch.zip) す。このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。
   * クラウドインフラストラクチャー 2.2.4 上のAdobe Commerce

## パッチの適用方法

手順については、サポートナレッジベースの [Adobe Commerceが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 添付ファイル
