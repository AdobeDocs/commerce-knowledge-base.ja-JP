---
title: Git からプッシュされると、新しい環境が実稼動環境に配置される
description: この記事では、Git バージョン管理システムからプッシュされた際に、新しい環境がクラウドインフラストラクチャ上のAdobe Commerce実稼動環境の下に配置される問題の解決策について説明します。
exl-id: 279cd6d8-fd45-45ba-8456-8b397a01976f
feature: Cloud, Paas
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Git からプッシュされると、新しい環境が実稼動環境に配置される

この記事では、Git バージョン管理システムからプッシュされた際に、新しい環境がクラウドインフラストラクチャ上のAdobe Commerce実稼動環境の下に配置される問題の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[ サポートされているすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。

## 問題

<u> 前提条件 </u>:

プロジェクトのローカル Git で制御されたクローンがある。

<u> 再現手順 </u>:

ステージングブランチから統合ブランチを作成する必要があります。

1. ローカルシェルで次のコマンドを実行して、ステージングブランチに切り替えます。`git checkout staging`
1. ローカルシェルで次のコマンドを実行して、ステージングブランチから統合ブランチを作成します。`git checkout -b <branch>`
1. ブランチをリモートリポジトリにプッシュし、ローカルシェルで次のコマンドを実行してアップストリームブランチを設定します。`git push --set-upstream origin <branch>`

<u> 期待される結果 </u>:

ステージングブランチの下に新しいブランチが作成されます。

<u> 実際の結果 </u>:

実稼動ブランチの下に新しいブランチが作成されました。

## 原因：

これはバグではありません。 別のブランチに親ブランチを設定する場合、マーチャントは magento-cloud CLI を使用する必要があります。

## 解決策

親ブランチは、マーチャントが新しく作成されたブランチをプッシュしてアクティブ化した後にのみ設定できます。 開発者向けドキュメントの [ クラウドインフラストラクチャー上のAdobe Commerce/Bitbucket の統合 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/dev-tools/integrations/bitbucket#create-a-cloud-branch) を参照してください。

サーバー上の既存のブランチの親を更新するには、magento-cloud CLI で `magento-cloud environment:info` コマンドを使用します。

使用例：

`magento-cloud environment:info parent Staging`

これにより、現在チェックアウトされているブランチの親ブランチが「ステージング」に設定されます。

## 関連資料

* [ クラウドインフラストラクチャー上のAdobe Commerce/magento-cloud CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview) 開発者向けドキュメント。
