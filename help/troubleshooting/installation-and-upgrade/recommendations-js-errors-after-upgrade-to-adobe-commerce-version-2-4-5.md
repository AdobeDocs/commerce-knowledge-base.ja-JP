---
title: '[!UICONTROL Recommendations] [!DNL JS] Adobe Commerce バージョン 2.4.5 へのアップグレード後にエラーが発生する'
description: この記事では、Adobe Commerce（すべてのデプロイメント方法）にアップグレードした後、[!UICONTROL Recommendations] 品モジュールに関連するエラーがコンソールに表示される場合に対処する  [!DNL JS]  策を説明します。
feature: Install, Upgrade
role: Developer
exl-id: 51d899eb-48f7-48c5-8bda-bd72a4d28945
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Adobe Commerce バージョン 2.4.5 へのアップグレード後に [!UICONTROL Recommendations] [!DNL JS] エラーが発生する

この記事では、Adobe Commerce（すべてのデプロイメント方法）にアップグレードした後、製品またはモジュール/ユニットに関連するエラーがコンソールに表示され [!DNL JS] い場合に [!UICONTROL Recommendations] いて対処方法を説明します。

現在、今後のバージョンでこの問題に対処する予定はありません。

## 影響を受けるバージョンと製品

* バージョン 2.4.5 へのアップグレード時のAdobe Commerce（すべてのデプロイメント方法）

## 問題

この問題は、ストアフロントの web ページで、のホームページページの一部の削除された製品 [!UICONTROL Recommendations] モジュール/ユニット（ブロックやウィジェット）が引き続き参照されている [!DNL CMS] とが原因です。

<u> 再現手順 </u>:

1. Adobe Commerce 2.4.5 へのアップグレード。
1. ストアフロントの Web ページにアクセスします。
1. マウスを右クリックし、**Inspect** を選択して、web ブラウザーで web インスペクターを開きます。
1. 「**[!UICONTROL Console]**」タブをクリックします。
1. [!DNL JS] のエラーを確認します。

<u> 期待される結果 </u>:

[!DNL JS] エラーなしでアップグレードが成功しました。

<u> 実際の結果 </u>:

Web ブラウザーコンソールには、様々なタイプの [!DNL JS] エラーが表示されます。

## 回避策

回避策として、ページで使用したすべての [!UICONTROL Recommendations] ユニットを確認し、削除したユニットを削除できます。
