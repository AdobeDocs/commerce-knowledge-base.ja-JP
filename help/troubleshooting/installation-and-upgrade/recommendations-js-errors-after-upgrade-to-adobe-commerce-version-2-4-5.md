---
title: Adobe Commerce バージョン 2.4.5へのアップグレード後の[!UICONTROL Recommendations] [!DNL JS]  エラー
description: この記事では、Adobe Commerceへのアップグレード後（すべてのデプロイメント方法）に、製品[!UICONTROL Recommendations] モジュールに関連するコンソールに [!DNL JS]  エラーが発生した場合の解決策を示します。
feature: Install, Upgrade
role: Developer
exl-id: 51d899eb-48f7-48c5-8bda-bd72a4d28945
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Adobe Commerce バージョン 2.4.5へのアップグレード後に[!UICONTROL Recommendations] [!DNL JS] エラーが発生しました

この記事では、Adobe Commerceへのアップグレード後（すべてのデプロイメント方法）に、製品[!UICONTROL Recommendations]のモジュール/ユニットに関連するコンソールで[!DNL JS]個のエラーが発生した場合の対処方法を説明します。

現時点では、今後のバージョンでこの問題に対処する計画はありません。

## 影響を受けるバージョンと製品

* バージョン 2.4.5にアップグレードする場合のAdobe Commerce（すべてのデプロイメント方法）

## イシュー

この問題は、ストアフロントのweb ページで、削除された製品[!UICONTROL Recommendations]個のモジュール/ユニット（ブロックまたはウィジェット）をホームページ [!DNL CMS]で引き続き参照していることが原因です。

<u>複製する手順</u>:

1. Adobe Commerce 2.4.5へのアップグレード
1. ストアフロントのweb ページにアクセスする。
1. マウスを右クリックし、**検査**&#x200B;を選択して、web ブラウザーでweb インスペクターを開きます。
1. 「**[!UICONTROL Console]**」タブをクリックします。
1. [!DNL JS] エラーを確認してください。

<u>期待される結果</u>:

[!DNL JS] エラーなしで正常にアップグレードされました。

<u>実際の結果</u>:

Web ブラウザーコンソールには、様々な種類の[!DNL JS] エラーが表示されます。

## 回避策

回避策として、ページで使用したすべての[!UICONTROL Recommendations] ユニットを確認し、削除されたユニットを削除できます。
