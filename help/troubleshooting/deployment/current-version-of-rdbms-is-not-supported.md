---
title: デプロイメント時の「現在のバージョンのRDBMSはサポートされていません」エラー
description: この記事では、デプロイメントが失敗し、デプロイログに次のエラーが発生した場合の解決策を示します。*現在のバージョンのRDBMSはサポートされていません*。
exl-id: e7300f64-5749-4de8-b4d2-bc4789437282
feature: Deploy
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%
---
# デプロイメント時の「現在のバージョンのRDBMSはサポートされていません」エラー

この記事では、デプロイメントが失敗し、デプロイログに次のエラーが発生した場合の解決策を示します。*現在のバージョンのRDBMSはサポートされていません*。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure, 2.3.0-2.3.7-p1, 2.4.0-2.4.3.

## イシュー

このエラーメッセージは、現在のMariaDB バージョンがアップグレードしようとしているAdobe Commerce バージョンでサポートされなくなり、MariaDBを互換性のあるバージョンにアップグレードする必要があることを意味します。


<u>複製する手順</u>:

展開を試みます。

<u>期待される結果</u>:

デプロイメントの成功：

<u>実際の結果</u>:

デプロイメントが失敗し、エラーメッセージが表示されます：*現在のバージョンのRDBMSはサポートされていません*。

## 原因

お使いのバージョンのMariaDBは、アップグレードしようとしているAdobe Commerceのバージョンと互換性がありません。

## Solution

アプリケーションをアップグレードする前に、MariaDB サービスを互換性のあるバージョンにアップグレードする必要があります。


Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ（およびスターターアーキテクチャのすべてのブランチ）の統合ブランチについては、開発者ドキュメントの[Configure Service](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/services-yaml)に従ってください。

Adobe Commerce on cloud infrastructure Pro プランのアーキテクチャのステージングと実稼動については、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を送信して、Adobe Commerce バージョンのアップグレードをデプロイする前にサービスのアップグレードをリクエストしてください。


## 関連トピックス

* ビルドとデプロイメントに関する[&#x200B; ベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/best-practices#best-practices)をご覧ください。
* [Adobe Commerce 2.3.5 アップグレード：サポート情報ベースの動的テーブル &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html)へのコンパクト化。
