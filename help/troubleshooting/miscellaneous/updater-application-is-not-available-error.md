---
title: 「アップデーターアプリケーションを使用できません」エラー」
description: この文書では、Web セットアップ ウィザードを使用してオンプレミスでAdobe Commerceを更新/インストールする際に発生する可能性のある「updater application is not available」という問題の解決策について説明します。
exl-id: 85e55ed8-0bc9-4378-b722-46be98ce2638
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 「アップデーターアプリケーションを使用できません」エラーが発生する

この文書では、Web セットアップ ウィザードを使用してオンプレミスでAdobe Commerceを更新/インストールする際に発生する可能性のある「updater application is not available」という問題の解決策について説明します。

## 問題

準備状況チェックでは、次のメッセージが表示されます。

![Screen_Shot_2019-08-29_at_1.39.12_PM.png](assets/Screen_Shot_2019-08-29_at_1.39.12_PM.png)

## 影響を受ける製品/バージョン

* Adobe Commerce オンプレミス 2.2.x、2.3.x
* Magento Open Source2.2.x, 2.3.x


## 解決策

この問題を解決するには、がであるかどうかを確認します。 `<magento_root>/update` ファイルおよびサブディレクトリを含むディレクトリ。 それ以外の場合は、を参照してください [アップデーターの設定](https://devdocs.magento.com/guides/v2.3/comp-mgr/updater/update-updater.html) 開発者向けドキュメントを参照してください。
