---
title: 一般的なカスタムモジュールのトラブルシューティングヘルプ
description: ここでは、Adobe Commerceのカスタムモジュールのトラブルシューティングに役立つ一般的なツールについて説明します。
exl-id: c6603a2b-dc98-4022-ab29-c081c2b07415
feature: Extensions
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 一般的なカスタムモジュールのトラブルシューティングヘルプ

ここでは、Adobe Commerceのカスタムモジュールのトラブルシューティングに役立つ一般的なツールについて説明します。

## 問題

カスタムモジュールの機能に問題があることに気付いた場合は、問題を示す明らかなエラーメッセージが表示されないので、インスタンスのログを確認します。

## 解決策

ログを調べ、カスタムモジュールの名前を持つエントリがエラー内にあるかどうかを確認します。  関連するエラーに応じて、ソリューションは自動的に表示される場合もあれば、ログを開く場合に、役立つAdobe Commerce ログ情報を含める必要が生じる場合もあります。 [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket). ログの場所と考えられる解決策に関する情報については、次の段落を参照してください。

### Adobe Commerce（すべてのデプロイメント方法）、Magento Open Source、すべての 2.X バージョン

1. ログの場所：
   * [クラウドインフラストラクチャー上のAdobe Commerceスタータープランアーキテクチャログ](/help/how-to/general/log-locations-directories-for-starter-plan.md) サポートナレッジベースで。
   * [Adobe Commerce on cloud infrastructure Pro プランアーキテクチャログ](/help/how-to/general/log-locations-directories-for-pro-plan-integration-staging-production.md) サポートナレッジベースで。
1. 見つかったエラーに応じて、カスタムモジュールを有効、無効またはアンインストールする場合は、次の記事でアクションの詳細を説明します。
   * [モジュールの有効化または無効化](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-subcommands-enable.html) 開発者向けドキュメントを参照してください。
   * [モジュールのアンインストール](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-uninstall-mods.html) 開発者向けドキュメントを参照してください。

### クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

1. ログの場所： [クラウドインフラストラクチャログのAdobe Commerce](https://devdocs.magento.com/guides/v2.3/cloud/trouble/environments-logs.html) 開発者向けドキュメントを参照してください。
1. 見つかったエラーに応じて、カスタムモジュールを有効、無効、またはアンインストールする場合は、開発者ドキュメントの次の記事でアクションの詳細を説明しています。
   * [拡張機能のインストール、管理、アップグレード](https://devdocs.magento.com/guides/v2.3/cloud/howtos/install-components.html).
   * [コンポーネントのデプロイメントの失敗](https://devdocs.magento.com/guides/v2.3/cloud/trouble/trouble_comp-deploy-fail.html).

## 関連資料

開発者向けドキュメントでは、

* [モジュールの概要](https://devdocs.magento.com/guides/v2.3/architecture/archi_perspectives/components/modules/mod_intro.html)
* [オプションのサンプルデータのインストール中にエラーが発生しました](https://devdocs.magento.com/guides/v2.3/install-gde/trouble/tshoot_sample-data.html)
* [例外処理](https://devdocs.magento.com/guides/v2.3/graphql/develop/exceptions.html)
* [インストール中の例外](https://devdocs.magento.com/guides/v2.3/install-gde/trouble/tshoot_exceptions.html)
* [モジュールマネージャーの実行](https://devdocs.magento.com/guides/v2.3/comp-mgr/module-man/compman-checklist.html)
* [モジュール設定ファイル](https://devdocs.magento.com/guides/v2.3/config-guide/config/config-files.html)
* [メモリ不足エラー](https://devdocs.magento.com/guides/v2.3/comp-mgr/trouble/cman/out-of-memory.html)
