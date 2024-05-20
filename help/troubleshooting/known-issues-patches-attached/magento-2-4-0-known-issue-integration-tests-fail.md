---
title: 「Adobe Commerce 2.4.0 の既知の問題：統合テストが失敗する」
description: ここでは、「Dotdigitalgroup\Email\Test\Integration\Model\Sync\Importer\ImporterFailedTest::setUp （）」の宣言が 2.4.0 で使用される PHPUnit 9 と互換性がないので、統合テストが失敗するAdobe Commerce 2.4.0 の問題に対するパッチを説明します。
exl-id: 8e0ca2da-81d9-4561-a009-593240f46e41
feature: Integration
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 の既知の問題：統合テストが失敗する

この記事では、の宣言が原因で統合テストが失敗するAdobe Commerce 2.4.0 の問題に対するパッチを提供します `Dotdigitalgroup\Email\Test\Integration\Model\Sync\Importer\ImporterFailedTest::setUp()` は、2.4.0 に使用される PHPUnit 9 とは互換性がありません。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.0

## 問題

<u>再現手順</u>

2.4.0 統合テストを実行します。

<u>期待される結果</u>

テストは成功。

<u>実際の結果</u>

*PHP 致命的エラー：Dotdigitalgroup\\Email\\Test\\Integration\\Model\\Sync\\Importer\\ImporterFailedTest::setUp （）の宣言は PHPUnit\\Framework\\TestCase::setUp （）: /var/www/vendor/dotmailer/dotmailer-magento2-extension/Test/Integration/Model/Sync/Importer/ImporterFailedTest.phpの 36 行目の void と互換性がある必要があります*

## 解決策

この記事で提供されているパッチを適用します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[BUNDLE-2684-composer.patch](assets/BUNDLE-2684-composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.0

## パッチの適用方法

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 手順については、サポートナレッジベースを参照してください。

## 添付ファイル
