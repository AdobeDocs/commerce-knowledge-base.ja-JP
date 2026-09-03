---
title: インストール xdebug最大関数のネスト レベル エラー
description: この記事では、インストール時にxdebug最大関数のネスト レベル エラーが発生する問題を修正します。
exl-id: 1f64a9bb-59a7-41df-92a4-890d9d32bcbe
feature: Install
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# インストール xdebug最大関数のネスト レベル エラー

この記事では、インストール時にxdebug最大関数のネスト レベル エラーが発生する問題を修正します。

## 詳細

Adobe Commerceのインストール中に、次のようなメッセージが表示されます。

`PHP Fatal error: Maximum function nesting level of '100' reached, aborting! in <path>/ClassLoader.php`

実稼動環境で`xdebug`を使用しないことを強くお勧めします。

## Solution

Adobe Commerceのインストールまたはインストール後のストアフロントまたはCommerce管理者へのアクセスに影響を与える可能性がある`xdebug`に既知の問題があります。

詳しくは、サポートナレッジベースの「[xdebug](/help/troubleshooting/miscellaneous/known-issues-that-affect-installation.md)に関する既知の問題」を参照してください。
