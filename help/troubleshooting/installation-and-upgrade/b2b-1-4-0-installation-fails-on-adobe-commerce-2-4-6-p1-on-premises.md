---
title: Adobe Commerce 2.4.6-p1 オンプレミスでの[!DNL B2B] 1.4.0のインストールが失敗する
description: この記事では、[!DNL B2B] バージョン 1.4.0のインストールが失敗するAdobe Commerce 2.4.6-p1 オンプレミスの問題に対する回避策について説明します。
feature: Install, Upgrade, B2B
role: Developer
exl-id: 4a557c13-7ec2-4cfe-b86e-bb0d1a441658
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
subfeature_v2:
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%
---
# Adobe Commerce 2.4.6-p1 オンプレミスでの[!DNL B2B] 1.4.0のインストールが失敗する

この記事では、[!DNL B2B] バージョン 1.4.0のインストールが失敗するAdobe Commerce 2.4.6-p1 オンプレミスの問題に対する回避策について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.6-p1 **オンプレミス**
* [!DNL B2B] バージョン 1.4.0

>[!NOTE]
>
>[!DNL B2B] バージョン 1.4.0は、**Adobe Commerce Cloud 2.4.6-p1**&#x200B;に正常にインストールされました。

## イシュー

<u>複製する手順</u>:

1. Adobe Commerce 2.4.6-p1をインストールします。

   ```bash
   m2install.sh -s composer --ee -v 2.4.6-p1
   ```

1. [!DNL B2B] バージョン 1.4.0をインストールしてみてください。

   ```bash
   composer require magento/extension-b2b:1.4.0
   ```

<u>期待される結果</u>:

[!DNL B2B] バージョン 1.4.0がAdobe Commerce 2.4.6-p1に正常にインストールされました。

<u>実際の結果</u>:

インストールは次のエラーで失敗します。

```bash
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - Root composer.json requires magento/extension-b2b 1.4.0 -> satisfiable by magento/extension-b2b[1.4.0].
    - magento/extension-b2b 1.4.0 requires magento/security-package-b2b 1.0.4-beta1 -> found magento/security-package-b2b[1.0.4-beta1] but it does not match your minimum-stability.


Installation failed, reverting ./composer.json and ./composer.lock to their original content.
```

## 回避策

[安定性タグ &#x200B;](https://getcomposer.org/doc/04-schema.md#package-links)を持つ[!DNL B2B] セキュリティパッケージの手動による依存関係を追加することで、Adobe Commerce 2.4.6-p1上の[!DNL B2B] バージョン 1.4.0を正常にインストールまたはアップグレードしました。

1. Adobe Commerce インストールディレクトリから、必要な依存関係で`composer.json`を更新します。

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

1. `composer.json`を更新して、[!DNL B2B] バージョン 1.4.0を追加します。

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

1. インストールまたはアップグレードプロセスを完了します。

   * [クラウド インフラストラクチャへの [!DNL B2B] のインストール](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/b2b-module.html?lang=ja)
   * [オンプレミスのインストール](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html?lang=ja)
