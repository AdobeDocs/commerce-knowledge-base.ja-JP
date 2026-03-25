---
title: Adobe Commerce アップグレード 2.4.3、2.3.7-p1 PHPの致命的なエラーのホットフィックス
description: この記事では、Adobe Commerce（すべてのデプロイメント方法）またはMagento Open Source 2.4.3または2.3.7-p1にアップグレードしようとすると、次のエラーが表示される場合の修正点について説明します。
exl-id: 1c472214-8387-403e-b2d2-d3f3c9e1da6a
feature: Install, Upgrade
role: Developer
source-git-commit: 1dcd003bd9b08741c0fba464f5520797cfaeccbb
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Adobe Commerce アップグレード 2.4.3、2.3.7-p1 PHPの致命的なエラーのホットフィックス

この記事では、Adobe Commerce（すべてのデプロイメント方法）またはMagento Open Source 2.4.3または2.3.7-p1にアップグレードしようとすると、次のエラーが表示される場合の修正点について説明します。

*PHPの致命的なエラー：検出されないエラー：&lt;...>/magento/vendor/magento/framework/Filesystem/Directory/DenyListPathValidator.php:74*&#x200B;で未定義の関数Magento\Framework\Filesystem\Directory\str_contains（）を呼び出しています

この問題は、2.4.4、2.4.3-p1、および2.3.7-p2 リリースの範囲で修正されます。

## 影響を受けるバージョンと製品

* 2.3.7-p1または2.4.3にアップグレードする場合のAdobe Commerce（すべてのデプロイメント方法）。
* 2.3.7-p1または2.4.3にアップグレードする場合のMagento Open Source

## イシュー

この問題は、新しいAdobe Commerce 2.4.3および2.3.7-p1 バージョンで、PHP 8のみを使用している場合に発生します。関数`str_contains`。 Adobe Commerce 2.4.3および2.3.7-p1はPHP 7.4とのみ互換性があるため、この関数は使用できません。

<u>複製する手順</u> :

Adobe Commerce 2.4.3または2.3.7-p1へのアップグレードを試みます。

<u>期待される結果：</u>

アップグレードに成功しました。

<u>実際の結果：</u>

PHPの致命的なエラー。

## Solution

回避策として、CLI/ターミナルで次のコマンドを実行します：`composer require symfony/polyfill-php80` Magento ルート フォルダーから、またはコンポーザーのパッチをインストールします。

2.4.3の問題を修正するには、Adobe Commerce（すべてのデプロイメント方法）とMagento Open Sourceのマーチャントがパッチを適用する必要があります。

[AC-384_Fix_Incompatible_PHP_Method__2.4.3_ce.patch](assets/AC-384__Fix_Incompatible_PHP_Method__2.4.3_ce.patch.zip)

2.3.7-p1の問題を修正するには、Adobe Commerce（すべてのデプロイメント方法）とMagento Open Sourceのマーチャントがパッチを適用する必要があります。

[AC-384__Fix_Incompatible_PHP_Method__2.3.7-p1_ce.patch](assets/AC-384__Fix_Incompatible_PHP_Method__2.3.7-p1_ce.patch.zip)

## パッチの適用方法

手順については、[Magento](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/how-to-apply-a-composer-patch-provided-by-magento)が提供するコンポーザーパッチの適用方法を参照してください。

## 関連トピックス

GitHub [Magento 2.4.3 EE #33680](https://github.com/magento/magento2/issues/33680)でサポートされていないPHP 8 コマンド
