---
title: デプロイ後に、env.php で.magento.env.yaml の変更が表示されない
description: この記事では、.magento.env.yaml ファイルの変更がデプロイメント後もapp/etc/env.phpに反映されない問題の解決策について説明します。
exl-id: 39ea7295-ba5a-40cc-bc68-a5e0b965c1a7
feature: Deploy
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# デプロイ後に、env.php で.magento.env.yaml の変更が表示されない

>[!NOTE]
>
>この問題がある場合は、ece-tools 2002.1.5 にアップグレードして修正してください。 2002.1.5 には、各デプロイメントの opcache をリセットする機能があるので、設定 `opcache.enable_cli=1` を変更する必要はありません。 アップグレードしない場合は、ソリューションで後述されている回避策の手順を実行する必要があります。

この記事では、ファイルの変更がデプロイメント後に `app/etc/env.php` に反映 `.magento.env.yaml` れない問題の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce（すべて [ サポート対象バージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)）。

## 問題

`.magento.env.yaml` ファイルで行った変更は、生成される `app/etc/env.php` には影響しません。

<u> 再現手順：</u>

`.magento.env.yaml` の値を変更してサーバーにプッシュします。サーバーは、現在チェックアウトされている環境の設定（およびデプロイメント設定）を定義する必要があります。 手順については、開発者向けドキュメントの [ 環境変数/変数のデプロイ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy) を参照してください。

<u> 期待される結果：</u>

`.magento.env.yaml` ファイルで行った変更は、生成される `app/etc/env.php` に影響します。

<u> 実際の結果：</u>

変更は、デプロイメント後の `app/etc/env.php` 変数には影響しません。

## 原因：

この問題は、`php.ini` ファイルの `opcache.enable_cli` パラメーターの値が正しくないことが原因で発生する可能性があります。

## 解決策

1. [Adobe Commerceのパフォーマンスのベストプラクティス/ソフトウェアの推奨事項 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/performance-best-practices/software) に従ってシステムが設定されていることを確認します。
1. `php.ini` `opcache.enable_cli` ディレクティブが `0` に設定されているかどうかを次のコマンドを実行して確認します：`php -i | grep opcache.enable_cli`
1. 出力が `opcache.enable_cli=1` のような場合は、プロジェクトのルートディレクトリにある `php.ini` ファイルを編集し、`opcache.enable_cli=1` を `opcache.enable_cli=0` に変更します。
1. プロジェクトを再デプロイします。

## 関連資料

* [Cloud for Adobe Commerce/ビルドとデプロイ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml)。
