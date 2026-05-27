---
title: Gitからプッシュされたときに実稼動環境に配置された新しい環境
description: この記事では、Gitのバージョン管理システムからプッシュすると、Adobe Commerce on cloud infrastructureの実稼動環境の下に新しい環境が配置される問題の解決策を提供します。
exl-id: 279cd6d8-fd45-45ba-8456-8b397a01976f
feature: Cloud, Paas
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Gitからプッシュされたときに実稼動環境に配置された新しい環境

この記事では、Gitのバージョン管理システムからプッシュすると、Adobe Commerce on cloud infrastructureの実稼動環境の下に新しい環境が配置される問題の解決策を提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。

## イシュー

<u>前提条件</u>:

プロジェクトのローカル Git制御クローンを作成します。

<u>複製する手順</u>:

ステージング ブランチから統合ブランチを作成する必要があります。

1. ローカル シェルで次のコマンドを実行して、ステージング ブランチに切り替えます：`git checkout staging`
1. ローカル シェルで次のコマンドを実行して、ステージング ブランチから統合ブランチを作成します：`git checkout -b <branch>`
1. ブランチをリモート リポジトリにプッシュし、ローカル シェルで次のコマンドを実行してアップストリーム ブランチを設定します：`git push --set-upstream origin <branch>`

<u>期待される結果</u>:

新しいブランチは、ステージングブランチの下に作成されます。

<u>実際の結果</u>:

新しいブランチは実稼動用ブランチの下に作成されました。

## 原因

バグではありません。 別のブランチの親ブランチを設定する場合、マーチャントはmagento-cloud CLIを使用する必要があります。

## Solution

親ブランチは、マーチャントが新しく作成したブランチをプッシュしてアクティブ化した後にのみ設定できます。 開発者向けドキュメントの「[&#x200B; クラウドインフラストラクチャ上のAdobe Commerce > Bitbucket統合](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/dev-tools/integrations/bitbucket#create-a-cloud-branch)」を参照してください。

サーバー上の既存のブランチの親を更新するには、magento-cloud CLIで`magento-cloud environment:info` コマンドを使用してください。

使用例：

`magento-cloud environment:info parent Staging`

これにより、現在チェックアウトされているブランチの親ブランチが「ステージング」に設定されます。

## 関連トピックス

* 開発者向けドキュメントの[Adobe Commerce on cloud infrastructure > magento-cloud CLI](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview)。
