---
title: Adobe Commerce アップグレード 2.4.3、2.3.7-p1 PHP 致命的なエラーのホットフィックス
description: 「この記事では、マーチャントがAdobe Commerce（すべてのデプロイメント方法）またはMagento Open Source 2.4.3 または 2.3.7-p1 にアップグレードしようとすると、次のエラーが表示される場合の対応策を説明します。」
exl-id: 1c472214-8387-403e-b2d2-d3f3c9e1da6a
feature: Install, Upgrade
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Adobe Commerce アップグレード 2.4.3、2.3.7-p1 PHP 致命的なエラーのホットフィックス

この文書では、マーチャントがAdobe Commerce（すべてのデプロイメント方式）またはMagento Open Source 2.4.3 または 2.3.7-p1 にアップグレードしようとすると、次のエラーが表示される問題を修正します。

*PHP 致命的エラー：キャッチされないエラー：&lt;...>/magento/vendor/magento/framework/Filesystem/Directory/DenyListPathValidator.php:74 の未定義の関数Magento\Framework\Filesystem\Directory\str_contains（）への呼び出し*

この問題は、2.4.4、2.4.3-p1 および 2.3.7-p2 リリースの範囲で修正されます。

## 影響を受けるバージョンと製品

* 2.3.7-p1 または 2.4.3 にアップグレードする場合のAdobe Commerce（すべてのデプロイメント方法）
* 2.3.7-p1 または 2.4.3 へのアップグレード時のMagento Open Source。

## 問題

この問題は、PHP 8 のみを使用するAdobe Commerce 2.4.3 および 2.3.7-p1 の新しいバージョンによって引き起こされ `str_contains` す。 Adobe Commerce 2.4.3 および 2.3.7-p1 は PHP 7.4 とのみ互換性があるため、この関数は使用できません。

<u> 再現手順 </u> :

Adobe Commerce 2.4.3 または 2.3.7-p1 へのアップグレードを試みます。

<u> 期待される結果：</u>

アップグレードに成功しました。

<u> 実際の結果：</u>

PHP の致命的なエラー。

## 解決策

対応策として、CLI/ターミナルでMagentoのルート フォルダから `composer require symfony/polyfill-php80` コマンドを実行するか、Composer パッチをインストールします。

2.4.3 の問題を修正するには、Adobe Commerce（すべてのデプロイメント方法）とMagento Open Sourceマーチャントにパッチを適用する必要があります。

[AC-384_Fix_Incompatible_PHP_Method__2.4.3_ce.patch](assets/AC-384__Fix_Incompatible_PHP_Method__2.4.3_ce.patch.zip)

2.3.7-p1 の問題を修正するには、Adobe Commerce（すべてのデプロイメント方法）とMagento Open Sourceマーチャントにパッチを適用する必要があります。

[AC-384__Fix_Incompatible_PHP_Method__2.3.7-p1_ce.patch](assets/AC-384__Fix_Incompatible_PHP_Method__2.3.7-p1_ce.patch.zip)

## パッチの適用方法

手順については、[Magentoが提供する Composer パッチの適用方法 &#x200B;](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 関連資料

GitHub [Magento 2.4.3 でサポートされていない PHP 8 コマンド EE #33680](https://github.com/magento/magento2/issues/33680)
