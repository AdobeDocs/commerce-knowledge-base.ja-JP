---
title: デプロイ後に、env.php で.magento.env.yaml の変更が表示されない
description: この記事では、.magento.env.yaml ファイルの変更がデプロイメント後もapp/etc/env.phpに反映されない問題の解決策について説明します。
exl-id: 39ea7295-ba5a-40cc-bc68-a5e0b965c1a7
feature: Deploy
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# デプロイ後に、env.php で.magento.env.yaml の変更が表示されない

>[!NOTE]
>
>この問題がある場合は、ece-tools 2002.1.5 にアップグレードして修正してください。 2002.1.5 には、各デプロイメントの opcache をリセットする機能があるので、設定を変更する必要はありません `opcache.enable_cli=1`. アップグレードしない場合は、ソリューションで後述されている回避策の手順を実行する必要があります。

この記事では、が変更されたときの問題の解決策について説明します `.magento.env.yaml` ファイルがに反映されない `app/etc/env.php` デプロイメント後。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce（すべて） [サポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)）に設定します。

## 問題

で加えられた変更 `.magento.env.yaml` ファイルはに影響しません `app/etc/env.php` 生成済み。

<u>再現手順：</u>

内の値を変更します `.magento.env.yaml` サーバーにプッシュし、現在チェックアウトされている環境の設定（およびデプロイメント設定）を定義する必要があります。 手順については、を参照してください [環境変数/変数のデプロイ](https://devdocs.magento.com/cloud/env/variables-deploy.html) 開発者向けドキュメントを参照してください。

<u>期待される結果：</u>

で加えられた変更 `.magento.env.yaml` ファイルの影響： `app/etc/env.php` 生成済み。

<u>実際の結果：</u>

変更は次には影響しません `app/etc/env.php` デプロイメント後の変数。

## 原因：

この問題は、の値が正しくないために発生した可能性があります `opcache.enable_cli` のパラメーター `php.ini` ファイル。

## 解決策

1. システムが次のように設定されていることを確認します。 [Adobe Commerceのパフォーマンスのベストプラクティス > ソフトウェアの推奨事項](https://devdocs.magento.com/guides/v2.4/performance-best-practices/software.html).
1. チェックする `opcache.enable_cli` ディレクティブ： `php.ini` はに設定されています。 `0` 次を実行します。 `php -i | grep opcache.enable_cli`
1. 出力が次のような場合 `opcache.enable_cli=1` 、を編集します `php.ini` プロジェクトのルートディレクトリにあるファイルと `opcache.enable_cli=1` 対象： `opcache.enable_cli=0`
1. プロジェクトを再デプロイします。

## 関連資料

* [Cloud for Adobe Commerce/ビルドとデプロイ](https://devdocs.magento.com/cloud/project/magento-env-yaml.html).
