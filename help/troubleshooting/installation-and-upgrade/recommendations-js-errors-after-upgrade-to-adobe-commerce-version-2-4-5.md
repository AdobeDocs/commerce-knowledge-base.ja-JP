---
title: '''[!UICONTROL Recommendations] [!DNL JS] Adobe Commerce バージョン 2.4.5''へのアップグレード後にエラーが発生しました'
description: この記事では、Adobe Commerceにアップグレードした後（すべてのデプロイメント方法）、次の状況に対する修正を提供します [!DNL JS] 製品に関連するコンソールのエラー [!UICONTROL Recommendations] モジュール。
feature: Install, Upgrade
role: Developer
exl-id: 51d899eb-48f7-48c5-8bda-bd72a4d28945
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# [!UICONTROL Recommendations] [!DNL JS] Adobe Commerce バージョン 2.4.5 へのアップグレード後にエラーが発生する

この記事では、Adobe Commerceにアップグレードした後（すべてのデプロイメント方法）、次の状況に対する修正を提供します [!DNL JS] 製品に関連するコンソールのエラー [!UICONTROL Recommendations] モジュール/ユニット。

現在、今後のバージョンでこの問題に対処する予定はありません。

## 影響を受けるバージョンと製品

* バージョン 2.4.5 へのアップグレード時のAdobe Commerce（すべてのデプロイメント方法）

## 問題

この問題は、ストアフロントの web ページで、削除された製品がまだ参照されていることで発生します [!UICONTROL Recommendations] ホームページ上のモジュール/ユニット（ブロックやウィジェット） [!DNL CMS].

<u>再現手順</u>:

1. Adobe Commerce 2.4.5 へのアップグレード。
1. ストアフロントの Web ページにアクセスします。
1. マウスを右クリックし、を選択します。 **Inspect** をクリックして、web ブラウザーで web インスペクターを開きます。
1. 「」をクリックします **[!UICONTROL Console]** タブ。
1. をレビュー [!DNL JS] エラー。

<u>期待される結果</u>:

アップグレードは正常に終了しました（はありません） [!DNL JS] エラー。

<u>実際の結果</u>:

複数の異なるタイプの [!DNL JS] エラーは web ブラウザーコンソールに表示されます。

## 回避策

回避策として、すべての [!UICONTROL Recommendations] ページで使用した単位を削除し、削除した単位を削除します。
