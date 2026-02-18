---
title: デプロイメント時の「現在のバージョンの RDBMS はサポートされていません」エラー
description: この記事では、デプロイメントが失敗し、デプロイログに「現在のバージョンの RDBMS はサポートされていません」というエラーが記録されている場合の解決策を説明します。
exl-id: e7300f64-5749-4de8-b4d2-bc4789437282
feature: Deploy
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '273'
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


クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャの統合ブランチ（およびスターターアーキテクチャのすべてのブランチ）については、開発者向けドキュメントの [&#x200B; サービスを設定 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/services-yaml) に従ってください。

Adobe Commerce on cloud infrastructure Pro プランアーキテクチャのステージングと実稼働については、Adobe Commerce バージョンのアップグレードをデプロイする前に [&#x200B; サポートチケットを送信 &#x200B;](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) してサービスのアップグレードをリクエストしてください。


## 関連資料

* 開発者向けドキュメントの [&#x200B; ビルドとデプロイメントのベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/best-practices#best-practices)。
* [Adobe Commerce 2.3.5 へのアップグレード：動的テーブルにコンパクト化 &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html) サポート情報ベースで行います。
