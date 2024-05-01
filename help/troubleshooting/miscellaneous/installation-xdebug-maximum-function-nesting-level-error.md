---
title: インストール xdebug maximum function nesting level エラー
description: この記事では、インストール中の xdebug の最大関数のネスト レベル エラーを修正します。
exl-id: 1f64a9bb-59a7-41df-92a4-890d9d32bcbe
feature: Install
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# インストール xdebug maximum function nesting level エラー

この記事では、インストール中の xdebug の最大関数のネスト レベル エラーを修正します。

## 詳細

Adobe Commerceのインストール中に、次のようなメッセージが表示されます。

`PHP Fatal error: Maximum function nesting level of '100' reached, aborting! in <path>/ClassLoader.php`

を使用しないことを強くお勧めします `xdebug` （実稼動環境の場合）

## 解決策

に既知の問題があります `xdebug` これは、Adobe Commerceのインストールに影響を与えたり、インストール後にストアフロントまたはCommerce管理者にアクセスしたりする可能性があります。

詳しくは、を参照してください [xdebug の既知の問題](/help/troubleshooting/miscellaneous/known-issues-that-affect-installation.md) サポートナレッジベースで。
