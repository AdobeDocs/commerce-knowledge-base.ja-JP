---
title: Composer install コマンドが.gitignore ファイルを上書きする、Adobe Commerce
description: この記事では、クラウドインフラストラクチャ 2.4.2-p1および2.3.7上のAdobe Commerceで、トラッキング対象の「.gitignore」ファイルがcomposerによって上書きされる場合の解決策を紹介します。
exl-id: b0604bae-d630-4292-88d7-6945db30fcf4
feature: Install, Upgrade
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%
---
# Composer install コマンドが.gitignore ファイルを上書きする、Adobe Commerce

この記事では、クラウドインフラストラクチャ 2.4.2-p1および2.3.7で、Adobe Commerce上のcomposerでトラッキング対象の`.gitignore` ファイルが上書きされる場合の解決策を紹介します。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure 2.4.2-p1および2.3.7。

## イシュー

composer install コマンドの実行中に`.gitignore` ファイルが上書きされています。

<u>複製する手順</u>:


1. ワークスペース用に空のディレクトリを作成します。
1. 次のコマンドをルートディレクトリで実行します。

   ```bash
   composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition:2.4.2-p1.
   ```

   \#または2.3.7

1. 次に、次のコマンドを実行します。
   1. `echo "/this/line/should/stay" >> .gitignore`
   1. `git init`
   1. `git add * && git add .*`
   1. `git commit -m "Init"` # リポジトリにコミットされたファイル
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

<u>期待される結果</u>:

`.gitignore`はコンポーザーによって上書きされません。

<u>実際の結果</u>:

コンポーザーのインストール実行ごとに`.gitignore`が上書きされます。

## Solution

カスタム `.gitignore file`を保持するには、`magento-deploy-ignore` セクションで無視する必要があります。

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


## 関連トピックス

* [&#x200B; トラッキングされた.gitignore ファイルがコンポーザーによって上書きされています！](https://github.com/magento/magento2/issues/32888) 新しいリポジトリを作成します。
