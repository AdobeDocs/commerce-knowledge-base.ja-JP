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

実稼動環境では使用しないことを強くお勧めします `xdebug`

## 解決策

`xdebug` には既知の問題があり、Adobe Commerceのインストールに影響を与えたり、インストール後にストアフロントまたはCommerce管理者にアクセスしたりする可能性があります。

詳しくは、サポートナレッジベースの [xdebug の既知の問題 ](/help/troubleshooting/miscellaneous/known-issues-that-affect-installation.md) を参照してください。
