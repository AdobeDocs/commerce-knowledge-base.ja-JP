---
title: 「デプロイメントに失敗しました：MDVA-43395 パッチを適用できません」
description: この記事では、MDVA-43395 パッチを適用しようとすると展開に失敗する問題の解決策を示します。
exl-id: 5341be3a-a9d7-4a4b-9755-8c585c6922a4
feature: Deploy
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 配置に失敗しました：MDVA-43395 パッチを適用できません

この記事では、MDVA-43395 パッチを適用しようとすると展開に失敗する問題の解決策を示します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 問題

MDVA-43395 パッチを適用できません。

## 原因：

クラウドマーチャントは、[magento/magento-cloud-patches 1.0.16](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/release-notes/cloud-patches#v1016) がインストールされていて、既にパッチが含まれている場合は、MDVA-43395 パッチを個別に適用する必要はありません。

## 解決策

この問題を解決するには、`m2-hotfixes` ディレクトリから MDVA-43395 および MDVA-43443 パッチを削除し、再デプロイします。

`m2-hotfixes` ディレクトリを介して MDVA-43443 パッチを適用できた場合でも、前述のように削除する必要があります。 今後のバージョンのAdobe Commerceでは、これらのパッチが既に含まれるので、後でアップグレードすると、デプロイメントが失敗する可能性があります。

パッチが適用されているかどうかを確認するには、`vendor/bin/magento-patches -n status |grep 43443` コマンドを実行します。
このような複数の結果が表示される場合は、`m2-hotfixes` のフォルダから MDVA-43443 パッチを削除する必要があります。

```bash
$ vendor/bin/magento-patches -n status |grep 43443
║ MDVA-43443              │ Parser token new fix                                         │ Other           │ Adobe Commerce Support │ Applied     │ Patch type: Required                                     ║
║ N/A                     │ ../m2-hotfixes/MDVA-43443_EE_2.4.2-p2_COMPOSER_v1.patch      │ Other           │ Local                  │ Applied     │ Patch type: Custom                                       ║
```

## 関連資料

* [Adobeが提供する Composer パッチをサポートナレッジベースに適用する方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md)。
* 開発者向けドキュメントの [Commerceのクラウドパッチ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/release-notes/cloud-patches#v1016)。
