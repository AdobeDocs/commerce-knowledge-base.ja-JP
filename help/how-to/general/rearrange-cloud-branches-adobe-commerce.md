---
title: Adobe Commerce上のクラウドのブランチの並べ替え
description: この記事では、Adobe Commerce上のクラウドブランチが正しい階層に従って整理されていない場合に、それらのブランチを並べ替えるために実行できる手順について説明します。 ブランチが正しい階層に整理されていない場合、正しい親ブランチに結合することはできません。既存の親ブランチに移動します。
exl-id: 4fc0de96-da66-4634-a38a-6a1536855f8f
feature: Cloud
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

1. [[!DNL Super User]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja) の役割が必要です。
1. magento-cloud [!DNL CLI] をインストールします（まだインストールしていない場合）。
1. 移動する必要があるブランチに対して、次のコマンドを実行します。
   `magento-cloud environment:info -e <branch to move> parent <target parent>`

注：新しいブランチを作成する際に、親ブランチを指定できます。 手順については、開発者向けドキュメントの [ ブランチ作成のスターターの取得 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/cli-branches) を参照してください。

`branch <environment-name> <parent-environment-ID>` magento-cloud 環境コマンドを使用して、新しい環境ブランチを作成できます。

新しい環境ブランチの作成とアクティブ化にはさらに時間がかかる場合があります。

## 関連資料

開発者向けドキュメントの [ を使用したブランチの管理  [!DNL CLI]](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/cli-branches) を参照してください。
