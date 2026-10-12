---
title: Composerの変更によりダウンロードに失敗する
description: この記事では、失敗したAdobe Commerceのダウンロードエラーと例外エラーの修正について説明します。
exl-id: 5abdab97-4b0c-466b-a68f-a2637d2826e5
feature: Configuration
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%
---
# Composerの変更によりダウンロードに失敗する

この記事では、失敗したAdobe Commerceのダウンロードエラーと例外エラーの修正について説明します。

## イシュー

ダウンロード中に、次のエラーが表示されます。

```php
[ErrorException]
  file_get_contents(app/etc/NonComposerComponentRegistration.php): failed to open stream: No such file or directory
```

## 原因

これは、コンポーザーの特定のバージョンでの変更が原因で発生します。 この問題を回避するには、Composerを以前のバージョンにダウングレードし、Adobe Commerceのダウンロードを再試行します。

## Solution

2015年11月21日から11月26日までのバージョンのComposerには、この問題があります。 この問題がComposer バージョンに関連することを確認するには、次のコマンドを入力します。

```php
composer -v
```

バージョンは次のように表示されます。

```php
Composer version 1.0-dev (2b14f0a047dd4f3545ec82381f65c36ea93a4c81) 2015-11-25 17:13:09
```

日付は2015-11-25で、Composerにこの問題があることを示します。

回避するには：

1. 次のいずれかの操作を行って、Composerのバージョンを変更し、Adobe Commerce ソフトウェアをダウンロードできるようにします。

   * 次のコマンドを使用してComposerをダウングレードします：`composer self-update 1.0.0-alpha11`。
   * Composerを2015年11月26日以降のバージョンにアップグレード：`composer self-update`。

1. Adobe Commerceのディレクトリとサブディレクトリを削除します。
1. `[composer create-project](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/composer)`または`[git clone](https://developer.adobe.com/commerce/contributor/guides/install/clone-repository/)`を使用して、ダウンロードを再試行してください。
1. Adobe Commerce ソフトウェアのダウンロードが完了したら、Composerを更新します：`composer self-update`。
