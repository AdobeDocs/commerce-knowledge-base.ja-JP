---
title: クラウドインフラストラクチャ上のAdobe Commerceでのデプロイメントのダウンタイムを短縮
description: メンテナンスのダウンタイムを大幅に短縮し、環境全体でストアを効率的に設定するために、Adobe Commerce on cloud infrastructure には**Configuration Management**機能が用意されています。 Cloud infrastructure 2.2.x 以降の実装でのAdobe Commerceの場合、この機能では、パイプラインのデプロイメントの概念とオプションを手順を減らしながらサポートします。
exl-id: fde3571c-d95c-4a9b-a024-3b29f9c491ab
feature: Build, Cloud, Configuration, Deploy
source-git-commit: 23d957ceac17f9989d14b215582304199d398545
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# クラウドインフラストラクチャ上のAdobe Commerceでのデプロイメントのダウンタイムを短縮

メンテナンスのダウンタイムを大幅に短縮し、環境全体でストアを効率的に設定するために、Adobe Commerce on cloud infrastructure には **Configuration Management** 機能が用意されています。 Cloud infrastructure 2.2.x 以降の実装でのAdobe Commerceの場合、この機能では、パイプラインのデプロイメントの概念とオプションを手順を減らしながらサポートします。

## 概要

Web ストアのデプロイには、次のような苦痛や時間がかかる問題があります。

* **すべての環境に同じ設定を適用する** 通常は、手動で、または複雑なデータベース更新を使用して、設定を入力します。 Configuration Management を使用すると、データベースから設定を 1 つのファイルにエクスポートし、後でローカル開発環境から統合、ステージングおよび実稼動にコードでプッシュできます。

* **静的コンテンツをデプロイする際のサイトのダウンタイム。** 通常、静的コンテンツは [ デプロイフェーズ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/deploy/process#deploy-phase-deploy-phase) でデプロイされます。 これには最大 30 分以上かかることがありますが、ビジネスでは受け入れられません。 Configuration Management は、静的コンテンツのデプロイメントを [ ビルドフェーズ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/deploy/process#build-phase-build-phase) に移行しますが、ダウンタイムは必要ありません。

## 技術バージョン

* 設定管理用のクラウドインフラストラクチャー **2.1.4** 以降でのAdobe Commerce
* 設定管理/パイプラインデプロイメント用のクラウドインフラストラクチャー **2.2** 以降でのAdobe Commerce

## 構成管理とは

簡単に言えば、Configuration Management （パイプラインのデプロイメントとも呼ばれます）プロセスは、クラウドインフラストラクチャ上のAdobe Commerceの実装（データベース）からすべての設定を 1 つの PHP ファイルに抽出します。 次に、ファイルを Git コミットに追加し、すべての環境にプッシュします。

これには次の利点があります。

* **すべての環境で一貫性のある設定：** 設定ファイルに書き出される設定はロックされ（Commerce管理の対応するフィールドは読み取り専用になります）、ファイルをすべての環境にプッシュする際に一貫性のある設定が保証されます。
* **ダウンタイムの短縮：** 静的ファイルのデプロイメントは、[ デプロイフェーズ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/deploy/process#deploy-phase-deploy-phase) （サイトをメンテナンスモードにする必要がある）から [ ビルドフェーズ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/deploy/process#build-phase-build-phase) （サイトがメンテナンスモードでない場合で、エラーや問題が発生してもダウンしない）に移行します。
* **機密データの保護：** cloud infrastructure 2.2 以降のAdobe Commerceでは、プロセスによって機密データ（例えば、payment gateway の資格情報）も `env.php` ファイルに書き出されます。 このファイルは、作成先の環境にのみ保存し、Git ブランチと一緒にプッシュしないでください。

デプロイメントに設定管理アプローチを適用することを強くお勧めします。

## 開発者向けドキュメントの設定管理

* [Configuration management for **2.1.X**](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html?lang=ja) and [example](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html?lang=ja) in the *Adobe Commerce on cloud infrastructure ガイド*
* [ クラウドインフラストラクチャー上の *Adobe Commerce ガイドの&#x200B;**2.2.X**](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html?lang=ja) および [ 例 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html?lang=ja) の設定管理*
* [ クラウドインフラストラクチャー上のAdobe Commerceのアップグレード ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version.html?lang=ja#upgrade-from-older-versions) トピックの *2.0.X または 2.1.X からのアップグレード* の節
* [2&rbrace; クラウドインフラストラクチャー上のAdobe Commerce設定ガイドのパイプラインのデプロイメント ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/overview.html?lang=ja) - クラウドインフラストラクチャー上のAdobe Commerceの場合、このガイドの手順に従う必要はありません **&#x200B;このコンテンツは参照専用です。 アドビでは既に、クラウドインフラストラクチャー上のAdobe Commerceにビルドサーバーや統合環境などを提供しています。
