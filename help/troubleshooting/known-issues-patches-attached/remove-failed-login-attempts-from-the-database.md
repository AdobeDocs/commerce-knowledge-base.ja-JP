---
title: 失敗したログイン試行をデータベースから削除
description: この記事では、既存の失敗したログイン資格情報をAdobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure データベースから削除する方法について説明します。 バージョン 2.2.10 以降および 2.3.3 以降では、添付のスクリプトのみを実行する必要があります。 古いバージョン 2.3.0～2.3.2-p2 の場合は、パッチを適用してログを停止し、添付のスクリプトを実行して、既存の失敗したログイン資格情報を削除する必要があります。
exl-id: 0d7e3674-3563-414f-86a2-297eb8104099
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---

# 失敗したログイン試行をデータベースから削除

>[!NOTE]
>
>この記事は 2020 年 4 月 13 日に更新され、DB\_CLEANUP\_SCRIPT\_v2という新しいスクリプトが追加されました。 添付のDB\_CLEANUP\_SCRIPT\_v2 スクリプトを使用して、追加のテーブルにある既存の失敗したログインデータを消去してください。 以前にDB\_CLEANUP\_SCRIPT\_v2を実行したことがある場合でも、追加のテーブルがクリーンアップされるようにするために、DB\_CLEANUP\_SCRIPT\_v1を使用する必要があります。

この記事では、既存の失敗したログイン資格情報をAdobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure データベースから削除する方法について説明します。 バージョン 2.2.10 以降および 2.3.3 以降では、添付のスクリプトのみを実行する必要があります。 古いバージョン 2.3.0～2.3.2-p2 の場合は、パッチを適用してログを停止し、添付のスクリプトを実行して、既存の失敗したログイン資格情報を削除する必要があります。

## **影響を受ける製品とバージョン**

* この問題は、Magento Open Source、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.2.x、2.3.x およびそれ以前のバージョンに影響します。
* Adobe Commerce 1.x デプロイメントは影響を受けません。

## 問題

2019 年に、Adobe Commerce 2.3.x と 2.2.x のデータベースにログイン試行の失敗を許可するバグがAdobe Commerceに報告されました。これを受けて、Adobe Commerceでは、Adobe Commerce 2.3.3 および 2.2.10 （2019 年 10 月リリース）でこの問題を修正しました。 このバグの修正により、失敗したログイン試行のログが停止されましたが、これらの現在のバージョンに更新する前に収集された情報は引き続き存在する可能性があります。 この最新の修正により、以前にログに記録されたログイン試行情報がある場合はクリアされます。   CVE-2019-8118 については、[ 一般的な脆弱性と曝露 ](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-8118) で説明および追跡されています。

## 解決策

添付されたスクリプトとパッチを使用する必要があるか、スクリプトのみを使用する必要があるかは、Adobe Commerceのバージョンによって異なります。

**Adobe CommerceおよびMagento Open Sourceのバージョン 2.3.0 ～ 2.3.2 ～ p2**

これらのバージョンの場合は、パッチを適用し、添付されたデータベースのクリーンアップスクリプトを実行して、継続的なログを終了し、ログを削除する必要があります。

1. Composer パッチを実行してログを停止します。 このパッチは記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンク [CLEANUP\_PATCH\_COMPOSER\_2.3.2.patch](assets/CLEANUP_PATCH_COMPOSER_2.3.2.patch.zip) をクリックします。 パッチの適用方法については、サポートナレッジベースの [Adobe Commerceが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

1. 次に、スクリプトを実行して、既存の失敗したログイン試行のデータベースをクリーンアップします。 このスクリプトは記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンク [DB\_CLEANUP\_SCRIPT\_v2.php](assets/DB_CLEANUP_SCRIPT_v2.php.zip) をクリックします。

手順については、[**スクリプトの実行方法**](/help/troubleshooting/known-issues-patches-attached/remove-failed-login-attempts-from-the-database.md#run_script) の節を参照してください。

**Adobe CommerceおよびMagento Open Sourceのバージョン 2.3.3 以降/2.2.10 以降**<br>
これらのバージョンに限り、以下のスクリプトを実行して古いログをクリアします（2019 年 10 月にリリースされた修正を通じて、これらのバージョンのログは以前に終了されました）。 このスクリプトは記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンク [DB\_CLEANUP\_SCRIPT\_v2.php](assets/DB_CLEANUP_SCRIPT_v2.php.zip) をクリックします。

手順については、サポートナレッジベースの [**スクリプトの実行方法**](/help/troubleshooting/known-issues-patches-attached/remove-failed-login-attempts-from-the-database.md#run_script) の節を参照してください。

**スクリプトの実行方法**

以下の手順に従ってスクリプトを実行してください。

1. `DB_CLEANUP_SCRIPT_v2.php` をAdobe CommerceまたはMagento Open Sourceインストールのルートディレクトリ（`app/bootstrap.php` を含むアプリと同じディレクトリ）に配置します。
1. ターミナルで次のコマンドを実行します：`php DB_CLEANUP_SCRIPT_v2.php`。データベースのクリーンアッププロセスが開始されます。

スクリプトの実行中に問題が発生した場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) するか、[security@magento.com](mailto:security@magento.com) 宛てにメールを送信してください。

**添付ファイル**

[CLEANUP\_PATCH\_COMPOSER\_2.3.2.patch](assets/CLEANUP_PATCH_COMPOSER_2.3.2.patch.zip)

[DB\_CLEANUP\_SCRIPT\_v2.php](assets/DB_CLEANUP_SCRIPT_v2.php.zip)
