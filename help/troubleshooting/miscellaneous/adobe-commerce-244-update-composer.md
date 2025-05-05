---
title: Adobe Commerce 2.4.4 へのアップグレード時の Composer プラグインの問題
description: ここでは、Adobe Commerce 2.4.3 以前からAdobe Commerce 2.4.4 以降（将来のバージョンがリリースされた場合）にアップグレードする際の、composer プラグインの問題を回避する方法について説明します。
exl-id: 7502ca9e-c307-4e8a-aa1d-4886e7be25da
feature: Upgrade
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Adobe Commerce 2.4.4 へのアップグレード時の Composer プラグインの問題

この文書では、Adobe Commerce 2.4.3 以前からAdobe Commerce 2.4.4 以降（将来のバージョンがリリースされた場合）にアップグレードする際の、Composer プラグインの問題を回避する方法について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス、2.4.4 以降（リリース時）にアップデートする際の任意のバージョン
* クラウドインフラストラクチャー上のAdobe Commerce、2.4.4 以降（リリース時）にアップデートする際の任意のバージョン
* Magento Open Source、2.4.4 以上にアップデートする際のすべてのバージョン（リリース時）

## 問題

2022 年 7 月以降にAdobe Commerce 2.4.4 以降にアップデートすると、プラグインに関して composer から警告が表示される場合があります。

<u> 再現手順 </u>:

前提条件：Adobe Commerce 2.4.3 以前がインストールされている。

1. [ アップグレードの実行 ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade.html?lang=ja) の説明に従って、アップグレードを開始します。
1. `composer update` コマンドを実行して、Adobe Commerce アプリケーションをアップグレードします。

<u> 期待される結果 </u>:

アップグレードが正常に終了しました。

<u> 実際の結果 </u>:

インストールが失敗し、次のようなエラーが表示されます。

```bash
Writing lock file
Installing dependencies from lock file (including require-dev)
Package operations: 591 installs, 0 updates, 0 removals
  - Installing laminas/laminas-dependency-plugin (2.2.0): Extracting archive
laminas/laminas-dependency-plugin contains a Composer plugin which is currently not in your allow-plugins config. See https://getcomposer.org/allow-plugins
Do you trust "laminas/laminas-dependency-plugin" to execute code and wish to enable it now? (writes "allow-plugins" to composer.json) [y,n,d,?] y
Plugin initialization failed (require(app/etc/NonComposerComponentRegistration.php): failed to open stream: No such file or directory), uninstalling plugin
  - Removing laminas/laminas-dependency-plugin (2.2.0)
    Install of laminas/laminas-dependency-plugin failed


  [ErrorException]
  require(app/etc/NonComposerComponentRegistration.php): failed to open stream: No such file or directory
```

## 原因：

2022 年 7 月以降、Composer は [`allow-plugins` オプションのデフォルト値を `{}` に変更し ](https://getcomposer.org/doc/06-config.md#allow-plugins) 許可されない限りプラグインは読み込まれません。

## 解決策

Adobe Commerceのインストール方法に応じて、`composer.json` ファイルに次の内容を追加します。

* プロジェクトが作成されている場合 [`composer create-project` コマンドを使用 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/composer#get-the-metapackage):

  ```json
  "config": {
      "allow-plugins": {
          "dealerdirect/phpcodesniffer-composer-installer": true,
          "laminas/laminas-dependency-plugin": true,
          "magento/*": true
      }
  }
  ```

* プロジェクトが別の方法で作成され、`"require-dev"` のセクションに `"dealerdirect/phpcodesniffer-installer"` がない場合：

  ```json
  "config": {
      "allow-plugins": {
          "laminas/laminas-dependency-plugin": true,
          "magento/*": true
      }
  }
  ```

`composer.json` ファイルを更新した後、`composer update` コマンドを実行し、アップグレードプロセスを再開します。
