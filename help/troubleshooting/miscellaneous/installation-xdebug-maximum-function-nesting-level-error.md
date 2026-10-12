---
title: インストール xdebug最大関数のネスト レベル エラー
description: この記事では、インストール時にxdebug最大関数のネスト レベル エラーが発生する問題を修正します。
exl-id: 1f64a9bb-59a7-41df-92a4-890d9d32bcbe
feature: Install
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
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
