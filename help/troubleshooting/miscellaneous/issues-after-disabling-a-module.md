---
title: モジュールを無効にした後の問題
description: この記事では、Commerce Admin でモジュール出力を無効にした後のモジュール機能の問題の解決策について説明します。
exl-id: 517f6993-f09e-4a94-8c57-175ecf9a98a8
feature: Extensions
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# モジュールを無効にした後の問題

この記事では、Commerce Admin でモジュール出力を無効にした後のモジュール機能の問題の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.1.X 以前のAdobe Commerce
* Adobe Commerce オンプレミス 2.1.X 以前

## 問題

Commerce管理者のでモジュール出力を無効にしている **ストア** > **設定** > **設定** > 詳細 > **詳細**&#x200B;を参照してください。モジュール機能に関連する問題が発生することがあります。

## 原因：

でのモジュール出力の無効化 **ストア** > **設定** > **設定** > 詳細 > **詳細** は出力（HTML、JS）のみを無効にしますが、このモジュールの機能は無効になりません。

## 解決策

モジュール機能を無効にする必要がある場合は、の説明に従って、モジュールを無効にします [モジュールの有効化または無効化](https://devdocs.magento.com/guides/v2.1/install-gde/install/cli/install-cli-subcommands-enable.html) 開発者向けドキュメントを参照してください。

モジュール出力の無効化機能は、バージョン 2.2.0 以降で削除されました。
