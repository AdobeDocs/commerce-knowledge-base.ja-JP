---
title: 一般的なカスタムモジュールのトラブルシューティングのヘルプ
description: この記事では、Adobe Commerceのカスタムモジュールのトラブルシューティングに役立つ一般的なツールについて説明します。
exl-id: c6603a2b-dc98-4022-ab29-c081c2b07415
feature: Extensions
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
subfeature_v2:
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
    internal-label: Extensions
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%
---
# 一般的なカスタムモジュールのトラブルシューティングのヘルプ

この記事では、Adobe Commerceのカスタムモジュールのトラブルシューティングに役立つ一般的なツールについて説明します。

## イシュー

カスタムモジュールの機能に問題があることに気づき、その問題を示す明らかなエラーメッセージが表示されない場合は、インスタンスのログを参照する必要があります。

## Solution

ログを確認して、カスタムモジュールの名前を持つエントリがエラーに含まれているかどうかを確認します。  関連するエラーによっては、解決策が表示される場合があります。また、[ サポートチケット ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を開く場合は、役に立つAdobe Commerce ログ情報を含める必要がある場合もあります。 ログの場所と考えられる解決策については、次の段落を参照してください。

### Adobe Commerce（すべてのデプロイメント方法）、Magento Open Source、すべての2.X バージョン

1. ログの場所は、Adobe Commerce on cloud infrastructure Pro プランアーキテクチャログ（サポートナレッジベース）に配置されます。
1. 見つかったエラーに応じて、カスタムモジュールを有効、無効、またはアンインストールする場合は、これらのアクションについて詳しく説明します。
   * [開発者向けドキュメントのモジュール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/manage-modules)を有効または無効にします。
   * 開発者向けドキュメントの[ モジュールのアンインストール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)。

### Adobe Commerceオンクラウドインフラストラクチャ（全バージョン）

1. ログの場所：[ クラウドインフラストラクチャ上のAdobe Commerceは、開発者ドキュメントのログ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations)です。
1. 見つかったエラーに応じて、カスタムモジュールを有効、無効、またはアンインストールする場合は、次の開発者向けドキュメントの記事で、これらのアクションについて詳しく説明しています。
   * [拡張機能のインストール、管理、アップグレード ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions)。
   * [ コンポーネントの展開エラー](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/recover-failed-deployment)。

## 関連トピックス

アドビの開発者ドキュメントには、次のようなものがあります。

* [モジュールの概要](https://developer.adobe.com/commerce/php/architecture/modules/overview/)
* [オプションのサンプルデータのインストール中にエラーが発生する](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/errors-installing-optional-sample-data)
* [例外処理](https://developer.adobe.com/commerce/webapi/graphql/develop/exceptions/)
* [インストール時の例外](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/exceptions-during-installation)
* [モジュールマネージャーの実行](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/prerequisites)
* [モジュール設定ファイル](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/files/module-files)
* [メモリ不足エラー](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/installation-and-upgrade/out-of-memory-error-during-install-or-upgrade)
