---
title: 「アップデーターアプリケーションを使用できません」エラー」
description: この文書では、Web セットアップ ウィザードを使用してオンプレミスでAdobe Commerceを更新/インストールする際に発生する可能性のある「updater application is not available」という問題の解決策について説明します。
exl-id: 85e55ed8-0bc9-4378-b722-46be98ce2638
feature: Configuration
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

この問題を解決するには、ファイルおよびサブディレクトリを含んだ `<magento_root>/update` ディレクトリがあるかどうかを確認します。 それ以外の場合は、開発者向けドキュメントの [ アップデーターの設定 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/updater-application-is-not-available-error) を参照してください。
