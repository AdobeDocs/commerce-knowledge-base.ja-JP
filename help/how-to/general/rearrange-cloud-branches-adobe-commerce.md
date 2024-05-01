---
title: Adobe Commerce上のクラウドのブランチの並べ替え
description: この記事では、Adobe Commerce上のクラウドブランチが正しい階層に従って整理されていない場合に、それらのブランチを並べ替えるために実行できる手順について説明します。 ブランチが正しい階層に整理されていない場合、正しい親ブランチに結合することはできません。既存の親ブランチに移動します。
exl-id: 4fc0de96-da66-4634-a38a-6a1536855f8f
feature: Cloud
source-git-commit: 83b21845cd306336e1cb193a9541478c8a38eea8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Adobe Commerce上のクラウドのブランチの並べ替え

この記事では、Adobe Commerce上のクラウドブランチが正しい階層に従って整理されていない場合に、それらのブランチを並べ替えるために実行できる手順について説明します。 ブランチが正しい階層に整理されていない場合、正しい親ブランチに結合することはできません。既存の親ブランチに移動します。

## 影響を受ける製品とバージョン：

* クラウドインフラストラクチャー上のAdobe Commerce, 2.3.0-2.3.7-p2, 2.4.0-2.4.3-p1

## クラウド分岐組織

ブランチの正しい階層組織は次のとおりです。

* [!DNL Master [main] > Production > Staging > Integration]
* [!DNL Master [main] > Production > Staging > Integration2]

## 間違ったクラウド分岐組織のソリューション

クラウドのブランチを並べ替えるには：

1. 以下が必要です。 [[!DNL Super User]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html) 役割。
1. magento-cloud のインストール [!DNL CLI] （まだ行っていない場合）。
1. 移動する必要があるブランチに対して、次のコマンドを実行します。
   `magento-cloud environment:info -e <branch to move> parent <target parent>`

注：新しいブランチを作成する際に、親ブランチを指定できます。 手順については、次を参照してください [分岐を作成するスターターを取得しています](https://devdocs.magento.com/cloud/env/environments-start.html#getstarted) 開発者向けドキュメントを参照してください。

新しい環境ブランチを作成するには、 `branch <environment-name> <parent-environment-ID>` magento-cloud 環境コマンド

新しい環境ブランチの作成とアクティブ化にはさらに時間がかかる場合があります。

## 関連資料

[を使用して分岐を管理する [!DNL CLI]](https://devdocs.magento.com/cloud/env/environments-start.html) 開発者向けドキュメントを参照してください。
