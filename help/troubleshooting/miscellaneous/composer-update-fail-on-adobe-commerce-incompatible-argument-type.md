---
title: 「Adobe Commerceで Composer の更新が失敗します：互換性のない引数タイプ」
description: この記事では、コードのコンパイルに問題があるためにデプロイメントが停止した場合の解決策を提供します。 この問題は、新しいバージョンの symfony/console 依存関係（4.4.27、4.4.28）によって発生します。
exl-id: ba2dd229-29f6-43e2-9467-8bd1bf59e6ef
feature: Console
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Adobe Commerceで Composer の更新に失敗します：互換性のない引数タイプです

>[!NOTE]
>
>この問題は、最新の symfony バージョン 4.4.29 リリースで修正されました。

この記事では、コードのコンパイルに問題があるためにデプロイメントが停止した場合の解決策を提供します。 この問題は、新しいバージョンの symfony/console 依存関係（4.4.27、4.4.28）によって発生します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）とMagento Open Source:
   * 2.4.0、2.4.0-p1、2.4.1、2.4.1-p1、2.4.2、2.4.2-p1、2.4.2-p2、2.4.3
   * 2.3.5、2.3.5-p1、2.3.5-p2、2.3.6、2.3.6-p1、2.3.7、2.3.7-p1
* symfony/console 依存関係（4.4.27、4.4.28）。

## 問題

symfony/console 依存関係の新しいバージョン（4.4.27、4.4.28）により、依存関係のコンパイル処理が失敗します。

<u> 再現手順 </u>:

Adobe Commerceをインストールまたはアップグレードする場合、または composer のアップデートを実行する場合は、次のエラーメッセージが表示されて実行が失敗します。
*互換性のない引数タイプ：必須タイプ : int。 実際のタイプ：文字列*

## 原因：

この問題は、バージョン 4.4.27 および 4.4.28 でリリースされた最新の「symfony/console」依存関係とのAdobe Commerce コアコードの非互換性が原因です。

## 解決策

この問題は、新しい symfony/console バージョン 4.2.29 （2021 年 8 月予定）がリリースされると、自動的に解決されます。

**オンプレミスのAdobe Commerceを修正する方法：**

Adobe Commerce オンプレミス 2.4.x

CLI/ターミナルで次のコマンドを実行します。

``composer require symfony/console:">=4.4.0 <4.4.27 || ~4.4.29"``

2.3.5 以降のAdobe Commerce オンプレミスのマーチャントは、すべて次の CLI コマンドを実行する必要があります。

``composer require symfony/console:"~4.1.0||~4.2.0||~4.3.0||>=4.4.0 <4.4.27 || ~4.4.29"``

**クラウドインフラストラクチャ上のAdobe Commerceを修正する方法：**

上記のコマンドを実行するか、7 月 29 日木曜日（PT）に利用可能になる最新バージョンの ECE ツール（ece-tools: 2002.1.7）にアップグレードします。 手順については、開発者向けドキュメントの [Cloud for Adobe Commerce/ece-tools バージョンの更新 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package) を参照してください。

完全な修正は、Adobe Commerce（すべてのデプロイメント方法） 2.4.4 でリリースされる予定です。

## 関連資料

* Github: [2021-07-27 Composer 更新互換性のない引数タイプ：必須タイプ : int。 実際のタイプ：文字列 ](https://github.com/magento/magento2/issues/33595)
