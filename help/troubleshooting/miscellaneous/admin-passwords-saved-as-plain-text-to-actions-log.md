---
title: 管理者パスワードがアクションログにプレーンテキストとして保存される
description: ここでは、Commerce管理者が管理者権限で新しいユーザーを作成し、パスワードが「magento_logging_event_changes」データベーステーブルにプレーンテキストとして保存される場合の修正点について説明します。
exl-id: 0e91198e-66b9-456a-9b75-5986369ed8e6
feature: Admin Workspace, Logs
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 管理者パスワードがアクションログにプレーンテキストとして保存される

ここでは、Commerce管理者が管理者権限で新しいユーザーを作成し、パスワードがにプレーンテキストとして保存される場合の修正点について説明します `magento_logging_event_changes` データベーステーブル。

このセキュリティの問題を修正するには、Adobe Commerce 2.0.16 および 2.1.9 セキュリティアップデートをインストールしてください。 セキュリティ更新プログラムを適用した後、パスワードは暗号化され、プレーンテキストとして表示されません。

## 影響を受けるバージョン {#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Affectedversions}

* Adobe Commerce オンプレミス 2.X.X
* クラウドインフラストラクチャー 2.X.X 上のAdobe Commerce

## 問題 {#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Issue}

既存のCommerce管理者が、 **システム** > **権限** > **すべてのユーザー** > **新しいユーザーを追加**&#x200B;を選択すると、パスワード（確認用に入力）がにプレーンテキストとして保存されます。 `magento_logging_event_changes` データベーステーブル。

### 再現手順： {#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Stepstoreproduce}

1. 管理者としてログインし、次のパスに移動して新しいユーザーを作成します。 **システム** > 権限 > **すべてのユーザー**.

   ![add_user_magento_2.4.1.png](assets/add_user_magento_2.4.1.png)

1. 次に、 **新しいユーザーを追加** ページ。 プロンプトが表示されたら、現在の管理者のパスワードを入力します。
1. に移動します **システム** > **アクションログ** > **報告書** 最後のログエントリに移動して検索します。
1. 暗号化もハッシュ化もされていない、現在のパスワードが表示されます。

## 解決策 {#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Solution}

のインストール [Adobe Commerce 2.0.16 および 2.1.9 セキュリティアップデート](https://magento.com/security/patches/magento-2016-and-219-security-update) この問題を修正します。

セキュリティアップデートのインストール後、パスワードが暗号化されるので、プレーンテキストでに表示されない `magento_logging_event_changes` テーブル。

## 詳細情報 {#Adminpasswordsaresavedasplaintexttoactionslog('magento_logging_event_changes'table)-Moreinformation}

[Adobe Commerce 2.0.16 および 2.1.9 セキュリティアップデート](https://magento.com/security/patches/magento-2016-and-219-security-update) 私たちのセキュリティセンターで。

[Adobe Commerce アプリケーションおよびコンポーネントのアップグレード](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/overview.html) 開発者向けドキュメントを参照してください。
