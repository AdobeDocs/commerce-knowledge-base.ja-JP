---
title: '''[!DNL B2B] Adobe Commerce 2.4.6-p1 オンプレミスで 1.4.0 のインストールが失敗する'
description: この記事では、Adobe Commerce 2.4.6-p1 オンプレミスの問題の回避策として、次の内容を説明します [!DNL B2B] バージョン 1.4.0 のインストールに失敗します。
feature: Install, Upgrade, B2B
role: Developer
exl-id: 4a557c13-7ec2-4cfe-b86e-bb0d1a441658
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# [!DNL B2B] Adobe Commerce 2.4.6-p1 オンプレミスで 1.4.0 のインストールが失敗する

この記事では、Adobe Commerce 2.4.6-p1 オンプレミスの問題の回避策として、次の内容を説明します [!DNL B2B] バージョン 1.4.0 のインストールに失敗します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.6-p1 **オンプレミス**
* [!DNL B2B] バージョン 1.4.0

>[!NOTE]
>
>[!DNL B2B] バージョン 1.4.0 はに正常にインストールされました **Adobe Commerce Cloud 2.4.6-p1**.

## 問題

<u>再現手順</u>:

1. Adobe Commerce 2.4.6-p1 をインストールします。

   ```terminal
   m2install.sh -s composer --ee -v 2.4.6-p1
   ```

1. インストールしてみる [!DNL B2B] バージョン 1.4.0。

   ```terminal
   composer require magento/extension-b2b:1.4.0
   ```

<u>期待される結果</u>:

[!DNL B2B] バージョン 1.4.0 がAdobe Commerce 2.4.6-p1 に正常にインストールされました。

<u>実際の結果</u>:

インストールが失敗し、次のエラーが表示されます。

```terminal
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - Root composer.json requires magento/extension-b2b 1.4.0 -> satisfiable by magento/extension-b2b[1.4.0].
    - magento/extension-b2b 1.4.0 requires magento/security-package-b2b 1.0.4-beta1 -> found magento/security-package-b2b[1.0.4-beta1] but it does not match your minimum-stability.


Installation failed, reverting ./composer.json and ./composer.lock to their original content.
```

## 回避策

へのインストールまたはアップグレードに成功しました [!DNL B2B] Adobe Commerce 2.4.6-p1 上のバージョン 1.4.0。手動で依存させる [!DNL B2B] を含むセキュリティパッケージ [安定性タグ](https://getcomposer.org/doc/04-schema.md#package-links).

1. Adobe Commerce インストールディレクトリから、を更新します `composer.json` 必要な依存関係を備えたもの：

   ```terminal
   composer require magento/module-re-captcha-company=1.0.3-beta1@beta magento/security-package-b2b=1.0.4-beta1@beta
   ```

   **コマンド出力：**

   ```terminal
   Running composer update magento/module-re-captcha-company magento/security-package-b2b
   Loading composer repositories with package information
   Updating dependencies
   Lock file operations: 2 installs, 0 updates, 0 removals
     - Locking magento/module-re-captcha-company (1.0.3-beta1)
     - Locking magento/security-package-b2b (1.0.4-beta1)
   Writing lock file
   Installing dependencies from lock file (including require-dev)
   Package operations: 2 installs, 0 updates, 0 removals
     - Downloading magento/module-re-captcha-company (1.0.3-beta1)
     - Installing magento/module-re-captcha-company (1.0.3-beta1): Extracting archive
     - Installing magento/security-package-b2b (1.0.4-beta1)
   1 package suggestions were added by new dependencies, use `composer suggest` to see details.
   Package sebastian/phpcpd is abandoned, you should avoid using it. No replacement was suggested.
   Generating autoload files
   132 packages you are using are looking for funding.
   Use the `composer fund` command to find out more!
   No security vulnerability advisories found
   ```

1. 更新 `composer.json` 追加 [!DNL B2B] バージョン 1.4.0。

   ```terminal
   composer require magento/extension-b2b=1.4.0
   ```

   **コマンド出力：**

   ```terminal
   ./composer.json has been updated
   Running composer update magento/extension-b2b
   Loading composer repositories with package information
   Updating dependencies
   ...
   Generating autoload files
   132 packages you are using are looking for funding.
   Use the `composer fund` command to find out more!
   No security vulnerability advisories found
   ```

1. インストールまたはアップグレードのプロセスを完了します。

   * [インストール [!DNL B2B] クラウドインフラストラクチャー上](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/b2b-module.html)
   * [オンプレミスでのインストール](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html)
