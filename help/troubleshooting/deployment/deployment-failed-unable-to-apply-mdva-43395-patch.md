---
title: 「デプロイメントに失敗しました：MDVA-43395 パッチを適用できません」
description: この記事では、MDVA-43395 パッチを適用しようとすると展開に失敗する問題の解決策を示します。
exl-id: 5341be3a-a9d7-4a4b-9755-8c585c6922a4
feature: Deploy
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
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

Cloud マーチャントは、以下の条件を満たす場合、MDVA-43395 パッチを個別に適用する必要はありません [magento/magento-cloud-patches 1.0.16](https://devdocs.magento.com/cloud/release-notes/mcp-release-notes.html#v1016) インストール済み。パッチは既に含まれています。

## 解決策

この問題を解決するには、から MDVA-43395 および MDVA-43443 パッチを削除します `m2-hotfixes` ディレクトリを作成して、再デプロイします。

MDVA-43443 パッチを経由して適用できた場合 `m2-hotfixes` ディレクトリを削除する必要があります（前述）。 今後のバージョンのAdobe Commerceでは、これらのパッチが既に含まれるので、後でアップグレードすると、デプロイメントが失敗する可能性があります。

パッチが適用されているかどうかを確認するには、 `vendor/bin/magento-patches -n status |grep 43443` コマンド。
このような複数の結果が表示される場合は、から MDVA-43443 パッチを削除してください。 `m2-hotfixes` フォルダー：

```bash
$ vendor/bin/magento-patches -n status |grep 43443
║ MDVA-43443              │ Parser token new fix                                         │ Other           │ Adobe Commerce Support │ Applied     │ Patch type: Required                                     ║
║ N/A                     │ ../m2-hotfixes/MDVA-43443_EE_2.4.2-p2_COMPOSER_v1.patch      │ Other           │ Local                  │ Applied     │ Patch type: Custom                                       ║
```

## 関連資料

* [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。
* [Commerceのクラウドパッチ](https://devdocs.magento.com/cloud/release-notes/mcp-release-notes.html#v1016) 開発者向けドキュメントを参照してください。
