---
title: '[!DNL Advanced Reporting] Adobe Commerceで 404 エラーが発生する'
description: Adobe Commerceこの文書では、マーチャントが [[!DNL Advanced Reporting]] （https://experienceleague.adobe.com/docs/commerce-admin/config/general/advanced-reporting.html）。 このパッチをインストールすると、ユーザーは以下にアクセスできるようになります [!DNL Advanced Reporting].
exl-id: bac61704-44fe-4bd2-b342-af90219231ef
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# [!DNL Advanced Reporting] Adobe Commerceの 404 エラー

この文書では、マーチャントがアクセスしようとしたときに 404 エラーが発生した場合のAdobe Commerceの問題に対するパッチを提供します [[!DNL Advanced Reporting]](https://experienceleague.adobe.com/docs/commerce-admin/config/general/advanced-reporting.html). このパッチをインストールすると、ユーザーは以下にアクセスできるようになります [!DNL Advanced Reporting].

このパッチでこの問題が解決されたかどうかを確認するには、まず次のコマンドを使用してログを確認します。

`zgrep analytics_collect_data var/log/support_report.log var/log/support_report.log.1.gz`

次の項目が表示された場合： `Not valid cipher` エラーが発生しました。添付されているパッチを適用してください。

## 影響を受ける製品とバージョン

Adobe Commerce 2.2.6

## 問題

マーチャントがアクセスしようとすると、404 エラーが発生する [!DNL Advanced Reporting].

## 解決策

この問題を修正するには、この記事に添付されているパッチを適用してください。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。 [MDVA-18980\_EE\_2.2.6\_COMPOSER\_v1 のダウンロード](assets/MDVA-18980_EE_2.2.6_COMPOSER_v1.patch.zip)

## パッチの適用方法

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 説明を参照してください。

## 添付ファイル
