---
title: Composer インストール コマンドが.gitignore ファイル、Adobe Commerceを上書きする
description: ここでは、トラッキング対象の「.gitignore」ファイルが、Adobe Commerce on cloud infrastructure 2.4.2-p1 および 2.3.7 上で composer によって上書きされた場合の解決策について説明します。
exl-id: b0604bae-d630-4292-88d7-6945db30fcf4
feature: Install, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Composer インストール コマンドが.gitignore ファイル、Adobe Commerceを上書きする

ここでは、トラッキング対象の `.gitignore` ファイルが、cloud infrastructure 2.4.2-p1 および 2.3.7 上のAdobe Commerce上の composer によって上書きされる場合の解決策について説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce 2.4.2-p1 および 2.3.7。

## 問題

composer`.gitignore` インストール コマンドを実行すると、ファイルが上書きされます。

<u> 再現手順 </u>:


1. ワークスペースに空のディレクトリを作成します。
1. ルートディレクトリで次のコマンドを実行します。

   ```bash
   composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition:2.4.2-p1.
   ```

   \#または 2.3.7

1. 次に、次のコマンドを実行します。
   1. `echo "/this/line/should/stay" >> .gitignore`
   1. `git init`
   1. `git add * && git add .*`
   1. `git commit -m "Init"` # ファイルがリポジトリにコミットされました
   1. `rm -rf vendor/*`
   1. `composer install`
   1. `git diff`

      ```git
      diff --git a/.gitignore b/.gitignore
      index c144521..7092a56 100644
      --- a/.gitignore
      +++ b/.gitignore
      @@ -70,4 +70,3 @@ atlassian*
      /generated/*
      !/generated/.htaccess
      .DS_Store
      -/this/line/should/stay
      ```

<u> 期待される結果 </u>:

`.gitignore` は作曲家によって上書きされません。

<u> 実際の結果 </u>:

`.gitignore` は、composer のインストールを実行するたびに上書きされます。

## 解決策

カスタム `.gitignore file` を保持するには、`magento-deploy-ignore` の節で無視する必要があります。

```git
{
...
"extra": {
    "magento-deploy-ignore": {
        "*": [
            "/.gitignore"
        ]
    }
    ...
}
```


## 関連資料

* [&#x200B; トラッキングされる.gitignore ファイルが composer によって上書きされます。Magento2 GitHub を &#x200B;](https://github.com/magento/magento2/issues/32888) きます。
