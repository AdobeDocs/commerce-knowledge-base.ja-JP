---
title: Composer の変更によりダウンロードが失敗する
description: この記事では、Adobe Commerceのダウンロードに失敗した場合の修正方法と例外エラーについて説明します。
exl-id: 5abdab97-4b0c-466b-a68f-a2637d2826e5
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Composer の変更によりダウンロードが失敗する

この記事では、Adobe Commerceのダウンロードに失敗した場合の修正方法と例外エラーについて説明します。

## 問題

ダウンロード中に、次のエラーが表示されます。

```php
[ErrorException]
  file_get_contents(app/etc/NonComposerComponentRegistration.php): failed to open stream: No such file or directory
```

## 原因：

これは、Composer の特定のバージョンの変更が原因で発生します。 これを回避するには、Composer を旧バージョンにダウングレードし、Adobe Commerceを再度ダウンロードします。

## 解決策

2015 年 11 月 21 日（PT）から 11 月 26 日（PT）までの Composer バージョンには、この問題があります。 この問題が Composer のバージョンに関連していることを確認するには、次のコマンドを入力します。

```php
composer -v
```

次のようなバージョンが表示されます。

```php
Composer version 1.0-dev (2b14f0a047dd4f3545ec82381f65c36ea93a4c81) 2015-11-25 17:13:09
```

日付は 2015-11-25 です。これは、Composer にこの問題があることを示しています。

この問題を回避するには：

1. Composer のバージョンを変更し、次のいずれかの操作を行ってAdobe Commerce ソフトウェアをダウンロードできるようにします。

   * 次のコマンドを使用して Composer をダウングレードします：`composer self-update 1.0.0-alpha11`。
   * Composer を 2015 年 11 月 26 日（PT）以降のバージョンにアップグレード：`composer self-update`

1. Adobe Commerce ディレクトリとサブディレクトリを削除します。
1. `[composer create-project](https://devdocs.magento.com/guides/v2.3/install-gde/composer.html)` または `[git clone](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/dev_install.html)` を使用して、もう一度ダウンロードしてみてください。
1. Adobe Commerce ソフトウェアのダウンロードが完了したら、Composer を更新します。`composer self-update`
