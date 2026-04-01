---
title: 一般的なカスタムモジュールのトラブルシューティングのヘルプ
description: この記事では、Adobe Commerceのカスタムモジュールのトラブルシューティングに役立つ一般的なツールについて説明します。
exl-id: c6603a2b-dc98-4022-ab29-c081c2b07415
feature: Extensions
role: Developer
source-git-commit: ae2a4508daeaf2d29a5f615918fcc46626b2e196
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 一般的なカスタムモジュールのトラブルシューティングのヘルプ

この記事では、Adobe Commerceのカスタムモジュールのトラブルシューティングに役立つ一般的なツールについて説明します。

## イシュー

カスタムモジュールの機能に問題があることに気づき、その問題を示す明らかなエラーメッセージが表示されない場合は、インスタンスのログを参照する必要があります。

## Solution

ログを確認して、カスタムモジュールの名前を持つエントリがエラーに含まれているかどうかを確認します。  関連するエラーによっては、解決策が表示される場合があります。また、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を開く場合は、役に立つAdobe Commerce ログ情報を含める必要がある場合もあります。 ログの場所と考えられる解決策については、次の段落を参照してください。

### Adobe Commerce（すべてのデプロイメント方法）、Magento Open Source、すべての2.X バージョン

1. ログの場所は、Adobe Commerce on cloud infrastructure Pro プランアーキテクチャログ（サポートナレッジベース）に配置されます。
1. 見つかったエラーに応じて、カスタムモジュールを有効、無効、またはアンインストールする場合は、これらのアクションについて詳しく説明します。
   * [開発者向けドキュメントのモジュール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/manage-modules)を有効または無効にします。
   * 開発者向けドキュメントの[&#x200B; モジュールのアンインストール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)。

### Adobe Commerceオンクラウドインフラストラクチャ（全バージョン）

1. ログの場所：[&#x200B; クラウドインフラストラクチャ上のAdobe Commerceは、開発者ドキュメントのログ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/test/log-locations)です。
1. 見つかったエラーに応じて、カスタムモジュールを有効、無効、またはアンインストールする場合は、次の開発者向けドキュメントの記事で、これらのアクションについて詳しく説明しています。
   * [拡張機能のインストール、管理、アップグレード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure-store/extensions)。
   * [&#x200B; コンポーネントの展開エラー](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/deploy/recover-failed-deployment)。

## 関連トピックス

アドビの開発者ドキュメントには、次のようなものがあります。

* [&#x200B; モジュールの概要](https://developer.adobe.com/commerce/php/architecture/modules/overview/)
* [&#x200B; オプションのサンプルデータのインストール中にエラーが発生しました](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/errors-installing-optional-sample-data)
* [例外処理](https://developer.adobe.com/commerce/webapi/graphql/develop/exceptions/)
* [&#x200B; インストール中に例外が発生しました](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/exceptions-during-installation)
* [&#x200B; モジュールマネージャーを実行](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/prepare/prerequisites)
* [&#x200B; モジュール設定ファイル &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/files/module-files)
* [&#x200B; メモリ不足エラー](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/out-of-memory-error-during-install-or-upgrade)
