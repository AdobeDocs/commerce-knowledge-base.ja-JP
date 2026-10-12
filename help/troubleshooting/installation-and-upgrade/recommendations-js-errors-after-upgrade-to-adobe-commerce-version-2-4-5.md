---
title: Adobe Commerce バージョン 2.4.5へのアップグレード後に[!UICONTROL Recommendations] [!DNL JS] エラーが発生しました
description: この記事では、Adobe Commerceへのアップグレード後（すべてのデプロイメント方法）に、製品[!UICONTROL Recommendations] モジュールに関連するコンソールに[!DNL JS]個のエラーが発生した場合の対処方法を説明します。
feature: Install, Upgrade
role: Developer
exl-id: 51d899eb-48f7-48c5-8bda-bd72a4d28945
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '197'
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
