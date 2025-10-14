---
title: 「Adobe Commerce 2.4.6-p1 オンプレミスで [!DNL B2B] 1.4.0 のインストールが失敗する」
description: この記事では、バージョン 1.4.0 のインストールに失敗したオンプレミス環境のAdobe Commerce 2 [!DNL B2B] 4.6-p1 の問題の回避策を提供します。
feature: Install, Upgrade, B2B
role: Developer
exl-id: 4a557c13-7ec2-4cfe-b86e-bb0d1a441658
source-git-commit: 35d4f2130d0ec71f71f5f20aa8a7c76207e7a35a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Adobe Commerce 2.4.6-p1 オンプレミスで [!DNL B2B] 1.4.0 のインストールが失敗する

この記事では、バージョン 1.4.0 のインストールに失敗したオンプレミス環境のAdobe Commerce 2.4.6-p1[!DNL B2B] 問題の回避策を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.6-p1 **オンプレミス**
* [!DNL B2B] バージョン 1.4.0

>[!NOTE]
>
>[!DNL B2B] バージョン 1.4.0 が **Adobe Commerce Cloud 2.4.6-p1** に正常にインストールされました。

## 問題

<u> 再現手順 </u>:

1. Adobe Commerce 2.4.6-p1 をインストールします。

   ```bash
   m2install.sh -s composer --ee -v 2.4.6-p1
   ```

1. [!DNL B2B] バージョン 1.4.0 をインストールしてみます。

   ```bash
   composer require magento/extension-b2b:1.4.0
   ```

<u> 期待される結果 </u>:

[!DNL B2B] バージョン 1.4.0 がAdobe Commerce 2.4.6-p1 に正常にインストールされました。

<u> 実際の結果 </u>:

インストールが失敗し、次のエラーが表示されます。

```bash
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - Root composer.json requires magento/extension-b2b 1.4.0 -> satisfiable by magento/extension-b2b[1.4.0].
    - magento/extension-b2b 1.4.0 requires magento/security-package-b2b 1.0.4-beta1 -> found magento/security-package-b2b[1.0.4-beta1] but it does not match your minimum-stability.


Installation failed, reverting ./composer.json and ./composer.lock to their original content.
```

## 回避策

[stability tag](https://getcomposer.org/doc/04-schema.md#package-links) を含む [!DNL B2B] セキュリティパッケージの手動依存関係を追加して、Adobe Commerce 2.4.6-p1 に [!DNL B2B] バージョン 1.4.0 を正常にインストールまたはアップグレードした。

1. Adobe Commerce インストールディレクトリから、必要な依存関係を使用して `composer.json` を更新します。

   ```bash
   composer require magento/module-re-captcha-company=1.0.3-beta1@beta magento/security-package-b2b=1.0.4-beta1@beta
   ```

   **コマンド出力：**

   ```bash
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

1. `composer.json` を更新して [!DNL B2B] バージョン 1.4.0 を追加します。

   ```bash
   composer require magento/extension-b2b=1.4.0
   ```

   **コマンド出力：**

   ```bash
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

   * [&#x200B; クラウドインフラストラ  [!DNL B2B]  チャへのインストール &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/b2b-module.html?lang=ja)
   * [&#x200B; オンプレミスでのインストール &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html?lang=ja)
