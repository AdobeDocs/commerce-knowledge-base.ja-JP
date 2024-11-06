---
title: Commerce管理のロックされた（グレー表示）フィールド
description: ここでは、Commerce管理者でフィールドを変更できない場合の解決策を説明します。
exl-id: 5fe0967a-4241-440b-bb0d-429fa5644bbc
feature: Admin Workspace
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Commerce管理のロックされた（グレー表示）フィールド

ここでは、Commerce管理者でロックされた（グレー表示されている）フィールドを変更できない場合の解決策を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.3.x、2.4.x
* クラウドインフラストラクチャー上のAdobe Commerce 2.3.x、2.4.x

## 問題

設定に対する変更を `app/etc/env.php` または `app/etc/config.php` に保存すると、管理者の設定を変更できなくなります。

<u> 再現手順 </u>:

メモ：これは例です。この問題は、保存されたすべての設定に影響を与える可能性があります。

1. マーチャントは、ターミナルで次のコマンドを使用して、配信方法の資格情報を保存します。`./vendor/bin/ece-tools config:dump`。 これにより、資格情報が `app/etc/env.php` ファイルに保存されます。
1. その後、マーチャントは後で資格情報の変更を試みます。

<u> 期待される結果 </u>:

マーチャントは、管理者フィールドの設定で値を設定して保存できます。

<u> 実際の結果 </u>:

管理者のフィールドはロックされています。または、値を変更できますが、管理者には保存されません。

## 原因：

設定が `env.php` または `config.php` に保存されると、管理者の設定を変更できなくなります。 設定の編集を許可するには、`env.php` または `config.php` から設定を削除する必要があります。

## 解決策

設定が `app/etc/env.php` または `app/etc/config.php` に保存されていないことを確認します。 保存されている場合は、次の手順を試してください。

* `config.php` – 設定を削除してから、再デプロイします。
* `env.php` - サーバー上で直接変更し、設定を削除してから、`bin/magento app:config:import` を実行します。

## 関連資料

* 開発者向けドキュメントの [ 設定を書き出す ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configuration-management/export-configuration) を参照してください。
* 開発者向けドキュメントの [ 設定値を設定 ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configuration-management/set-configuration-values) します。
* [ クラウドインフラストラクチャー上のAdobe Commerce:Configuration Management](/help/how-to/general/magento-cloud-reduce-deployment-downtime-with-configuration-management.md) を使用して、デプロイメントのダウンタイムを短縮できます。
