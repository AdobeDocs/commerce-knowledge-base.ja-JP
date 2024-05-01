---
title: Commerce Admin でロックされたフィールド
description: ここでは、Commerce管理者でフィールドを変更できない場合の解決策を説明します。
exl-id: 5fe0967a-4241-440b-bb0d-429fa5644bbc
feature: Admin Workspace
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Commerce Admin でロックされたフィールド

ここでは、Commerce管理者でフィールドを変更できない場合の解決策を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.3.x、2.4.x
* クラウドインフラストラクチャー上のAdobe Commerce 2.3.x、2.4.x

## 問題

設定に対する変更をに保存したら、 `app/etc/env.php` または `app/etc/config.php`ただし、管理者の設定を変更することはできません。

<u>再現手順</u>:

メモ：これは例です。この問題は、保存されたすべての設定に影響を与える可能性があります。

1. マーチャントは、ターミナルで次のコマンドを使用して、配信方法の資格情報を保存します。 `./vendor/bin/ece-tools config:dump`. これにより、資格情報がに保存されます `app/etc/env.php` ファイル。
1. その後、マーチャントは後で資格情報の変更を試みます。

<u>期待される結果</u>:

マーチャントは、管理者フィールドの設定で値を設定して保存できます。

<u>実際の結果</u>:

管理者のフィールドはロックされています。または、値を変更できますが、管理者には保存されません。

## 原因：

設定の保存先 `env.php` または `config.php`の場合、管理者の設定を変更することはできません。 設定の編集を許可するには、以下から設定を削除する必要があります。 `env.php` または `config.php`.

## 解決策

設定がに保存されていないことを確認します `app/etc/env.php` または `app/etc/config.php`. 保存されている場合は、次の手順を試してください。

* `config.php`  – 設定を削除してから、再デプロイします。
* `env.php` - サーバー上で直接変更し、設定を削除してから、を実行します `bin/magento app:config:import`.

## 関連資料

* [設定のエクスポート](https://devdocs.magento.com/guides/v2.4/config-guide/cli/config-cli-subcommands-config-mgmt-export.html#sensitive-or-system-specific-settings) 開発者向けドキュメントを参照してください。
* [設定値を設定](https://devdocs.magento.com/guides/v2.4/config-guide/cli/config-cli-subcommands-config-mgmt-set.html#config-cli-config-set) 開発者向けドキュメントを参照してください。
* [クラウドインフラストラクチャー上のAdobe Commerce：構成管理を使用したデプロイメントのダウンタイムの短縮](/help/how-to/general/magento-cloud-reduce-deployment-downtime-with-configuration-management.md) サポートナレッジベースで。
