---
title: 分割データベースソリューションの高度なレポート 404 エラー
description: この記事では、高度なレポートを使用しようとすると 404 エラーが発生する [split database solution] （https://devdocs.magento.com/guides/v2.3/config-guide/multi-master/multi-master.html）のAdobe Commerce 2.3.x ユーザー向けのパッチを提供します。
exl-id: b81d4ada-5f38-4882-bc5b-ab4ccd63fc5f
feature: Commerce Intelligence
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 分割データベースソリューションの高度なレポート 404 エラー

この記事では、を使用するAdobe Commerce 2.3.x ユーザー向けのパッチを提供します。 [データベース分割ソリューション](https://devdocs.magento.com/guides/v2.3/config-guide/multi-master/multi-master.html) 高度なレポートを使用しようとすると、404 エラーが発生する。

## 影響を受ける製品とバージョン

Adobe Commerce 2.3.0 - 2.3.5-p1

## 問題

このパッチは、間違った接続名を使用して引用符データを収集する問題を修正します。 誤った接続名が使用されているため、見積もりデータがMagento Business Intelligence（MBI）に送信されず、レポートを生成できません。

## 解決策

を適用 [パッチ](assets/MDVA-26831_EE_2.3.4_v1.composer.patch.zip) この条に規定する。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、次のリンクをクリックします。

[MDVA-26831\_EE\_2.3.4\_v1.composer.patch](assets/MDVA-26831_EE_2.3.4_v1.composer.patch.zip)

## パッチの適用方法

ファイルを解凍し、の指示に従います。 [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md).
