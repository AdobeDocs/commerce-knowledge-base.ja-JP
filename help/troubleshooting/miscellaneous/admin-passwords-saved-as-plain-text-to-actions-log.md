---
title: 管理者パスワードがアクションログにプレーンテキストとして保存される
description: ここでは、Commerce管理者が管理者権限で新しいユーザーを作成し、パスワードが「magento_logging_event_changes」データベーステーブルにプレーンテキストとして保存される場合の修正点について説明します。
exl-id: 0e91198e-66b9-456a-9b75-5986369ed8e6
feature: Admin Workspace, Logs
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 管理者パスワードがアクションログにプレーンテキストとして保存される

ここでは、Commerce管理者が管理者権限で新しいユーザーを作成し、パスワードがプレーンテキストとして `magento_logging_event_changes` データベーステーブルに保存される場合の修正点について説明します。

このセキュリティの問題を修正するには、Adobe Commerce 2.0.16 および 2.1.9 セキュリティアップデートをインストールしてください。 セキュリティ更新プログラムを適用した後、パスワードは暗号化され、プレーンテキストとして表示されません。

## 影響を受けるバージョン {#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Affectedversions}

* Adobe Commerce オンプレミス 2.X.X
* クラウドインフラストラクチャー 2.X.X 上のAdobe Commerce

## 問題 {#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Issue}

既存のCommerce管理者が **System**/**Permissions**/**All Users**/**Add new user** で Administrator 権限を持つ新しいユーザーを作成すると、パスワード（確認として入力）は `magento_logging_event_changes` データベーステーブルにプレーンテキストとして保存されます。

### 再現手順：{#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Stepstoreproduce}

1. 管理者としてログインし、**システム**/権限/**すべてのユーザー** のパスに移動して新しいユーザーを作成します。

   ![add_user_magento_2.4.1.png](assets/add_user_magento_2.4.1.png)

1. 次に、「**新しいユーザーを追加** ページをクリックします。 プロンプトが表示されたら、現在の管理者のパスワードを入力します。
1. **システム**/**アクションログ**/**レポート** ページに移動し、最後のログエントリを見つけます。
1. 暗号化もハッシュ化もされていない、現在のパスワードが表示されます。

## ソリューション {#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Solution}

[Adobe Commerce 2.0.16 および 2.1.9 セキュリティアップデートをインストールすると ](https://magento.com/security/patches/magento-2016-and-219-security-update) この問題が修正されます。

セキュリティ更新プログラムのインストール後、パスワードが暗号化され、`magento_logging_event_changes` テーブルにプレーンテキストで表示されなくなります。

## の詳細 {#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Moreinformation}

* [ セキュリティセンターのAdobe Commerce 2.0.16 および 2.1.9 セキュリティアップデート ](https://magento.com/security/patches/magento-2016-and-219-security-update) ページ
* 開発者向けドキュメントの [Adobe Commerce アプリケーションとコンポーネントのアップグレード ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/overview.html)
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
