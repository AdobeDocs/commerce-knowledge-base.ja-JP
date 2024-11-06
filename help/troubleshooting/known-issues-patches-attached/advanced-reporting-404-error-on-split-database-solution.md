---
title: 分割データベースソリューションの高度なレポート 404 エラー
description: この記事では、高度なレポートを使用しようとすると 404 エラーが発生する [split database solution] （https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/split-db/multi-master）のAdobe Commerce 2.3.x ユーザー向けのパッチを提供します。
exl-id: b81d4ada-5f38-4882-bc5b-ab4ccd63fc5f
feature: Commerce Intelligence
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 分割データベースソリューションの高度なレポート 404 エラー

この記事では、Adobe Commerce 2.3.x で [split database solution](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/split-db/multi-master) を使用していて、高度なレポートを使用しようとすると 404 エラーが発生するパッチを提供します。

## 影響を受ける製品とバージョン

Adobe Commerce 2.3.0 - 2.3.5-p1

## 問題

このパッチは、間違った接続名を使用して引用符データを収集する問題を修正します。 誤った接続名が使用されているため、見積もりデータがMagento Business Intelligence（MBI）に送信されず、レポートを生成できません。

## 解決策

この記事で提供されている [ パッチ ](assets/MDVA-26831_EE_2.3.4_v1.composer.patch.zip) を適用します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、次のリンクをクリックします。

[MDVA-26831\_EE\_2.3.4\_v1.composer.patch](assets/MDVA-26831_EE_2.3.4_v1.composer.patch.zip)

## パッチの適用方法

ファイルを解凍し、[Adobeが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) の手順に従います。
