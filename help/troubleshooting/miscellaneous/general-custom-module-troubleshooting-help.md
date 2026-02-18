---
title: 一般的なカスタムモジュールのトラブルシューティングヘルプ
description: ここでは、Adobe Commerceのカスタムモジュールのトラブルシューティングに役立つ一般的なツールについて説明します。
exl-id: c6603a2b-dc98-4022-ab29-c081c2b07415
feature: Extensions
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 一般的なカスタムモジュールのトラブルシューティングヘルプ

ここでは、Adobe Commerceのカスタムモジュールのトラブルシューティングに役立つ一般的なツールについて説明します。

## 問題

カスタムモジュールの機能に問題があることに気付いた場合は、問題を示す明らかなエラーメッセージが表示されないので、インスタンスのログを確認します。

## 解決策

ログを調べ、カスタムモジュールの名前を持つエントリがエラー内にあるかどうかを確認します。  発生したエラーに応じて、ソリューションが自動的に表示される場合もあれば、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) を開く場合に、役立つAdobe Commerce ログ情報を含める必要が生じる場合もあります。 ログの場所と考えられる解決策に関する情報については、次の段落を参照してください。

### Adobe Commerce（すべてのデプロイメント方法）、Magento Open Source、すべての 2.X バージョン

1. ログの場所は、サポートナレッジベースの [&#x200B; クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャログ &#x200B;](/help/how-to/general/log-locations-directories-for-pro-plan-integration-staging-production.md) にあります。
1. 見つかったエラーに応じて、カスタムモジュールを有効、無効またはアンインストールする場合は、次の記事でアクションの詳細を説明します。
   * 開発者向けドキュメントの [&#x200B; モジュールの有効化または無効化 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/manage-modules) を参照してください。
   * 開発者向けドキュメントの [&#x200B; モジュールをアンインストールする &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) を参照してください。

### クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

1. ログの場所：[&#x200B; クラウドインフラストラクチャログのAdobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations) に関する情報については、開発者向けドキュメントを参照してください。
1. 見つかったエラーに応じて、カスタムモジュールを有効、無効、またはアンインストールする場合は、開発者ドキュメントの次の記事でアクションの詳細を説明しています。
   * [&#x200B; 拡張機能のインストール、管理、アップグレード &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions)。
   * [&#x200B; コンポーネントのデプロイメントに失敗しました &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/recover-failed-deployment)。

## 関連資料

開発者向けドキュメントでは、

* [&#x200B; モジュールの概要 &#x200B;](https://developer.adobe.com/commerce/php/architecture/modules/overview/)
* [&#x200B; オプションのサンプルデータをインストール中にエラーが発生する &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/errors-installing-optional-sample-data)
* [&#x200B; 例外処理 &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/develop/exceptions/)
* [&#x200B; インストール中の例外 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/exceptions-during-installation)
* [&#x200B; モジュールマネージャーの実行 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/prerequisites)
* [&#x200B; モジュール設定ファイル &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/files/module-files)
* [&#x200B; メモリ不足エラー &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/out-of-memory-error-during-install-or-upgrade)
