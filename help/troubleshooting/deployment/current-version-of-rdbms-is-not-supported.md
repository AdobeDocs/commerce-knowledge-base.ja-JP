---
title: デプロイメント時の「現在のバージョンの RDBMS はサポートされていません」エラー
description: 「この記事では、デプロイメントが失敗し、デプロイログに「現在のバージョンの RDBMS はサポートされていません」というエラーが表示される場合の解決策を説明します。」
exl-id: e7300f64-5749-4de8-b4d2-bc4789437282
feature: Deploy
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# デプロイメント時の「現在のバージョンの RDBMS はサポートされていません」エラー

この記事では、デプロイが失敗し、デプロイログに *現在のバージョンの RDBMS はサポートされていません* というエラーが発生した場合の解決策を説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce, 2.3.0-2.3.7-p1, 2.4.0-2.4.3.

## 問題

このエラーメッセージは、現在の MariaDB のバージョンは、アップグレード先のAdobe Commerceのバージョンではサポートされなくなっており、MariaDB を互換性のあるバージョンにアップグレードする必要があることを示しています。


<u> 再現手順 </u>:

デプロイを試みます。

<u> 期待される結果 </u>:

正常なデプロイメント。

<u> 実際の結果 </u>:

デプロイメントが失敗し、次のエラーメッセージが表示されます。*現在のバージョンの RDBMS はサポートされていません*。

## 原因：

お使いの MariaDB のバージョンは、アップグレードしようとしているAdobe Commerceのバージョンと互換性がありません。

## 解決策

アプリケーションをアップグレードする前に、MariaDB サービスを互換性のあるバージョンにアップグレードする必要があります。


クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャの統合ブランチ（およびスターターアーキテクチャのすべてのブランチ）については、開発者向けドキュメントの [ サービスを設定 ](https://devdocs.magento.com/cloud/project/services.html) に従ってください。

Adobe Commerce on cloud infrastructure Pro プランアーキテクチャのステージングと実稼働については、Adobe Commerce バージョンのアップグレードをデプロイする前に [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してサービスのアップグレードをリクエストしてください。


## 関連資料

* 開発者向けドキュメントの [ ビルドとデプロイメントのベストプラクティス ](https://devdocs.magento.com/cloud/reference/discover-deploy.html#best-practices)。
* [Adobe Commerce 2.3.5 へのアップグレード：動的テーブルにコンパクト化 ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html) サポート情報ベースで行います。
