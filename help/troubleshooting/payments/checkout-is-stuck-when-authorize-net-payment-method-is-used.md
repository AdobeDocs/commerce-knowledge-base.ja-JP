---
title: Authorize.netのお支払い方法を使用すると、チェックアウトが停止する
description: この記事では、Adobe Commerce 2.3.Xの問題の説明と解決方法を説明します。Authorize.netを使用すると、ブラウザーコンソールのログに「*'Cannot read property 'length' of null'*」というエラーメッセージが表示され、チェックアウトが停止します。
exl-id: 01dc1147-4010-4dc5-81f3-3b3015a8c47c
feature: Cache, Checkout, Console, Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Authorize.netのお支払い方法を使用すると、チェックアウトが停止する

この記事では、Authorize.netを使用するとチェックアウトが停止するAdobe Commerce 2.3.Xの問題について説明し、ブラウザーコンソールのログに「*&#39;Cannot read property &#39;length&#39; of null&#39;*」というエラーメッセージが表示される場合の対処方法を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.3.X

>[!NOTE]
>
>コア Adobe Commerce Authorize.Net支払い統合は2.3.4以降で廃止され、2.4.0で完全に削除されました。 代わりに、[Adobe Commerce [!DNL Marketplace]](https://commercemarketplace.adobe.com/)のニーズに合った拡張機能を使用してください。

## イシュー

<u>複製する手順</u>

1. Commerce AdminでAuthorize.net支払い方法を設定します。
1. ストアフロントに移動します。
1. 商品をカートに追加し、チェックアウトに進みます。
1. 支払い方法としてAuthorize.netを選択します。
1. 「**注文を配置**」をクリックします。

<u>期待される結果</u>

Authorize.net iframeが読み込まれます。

<u>実際の結果</u>

Ajax スピナーが表示され、ページが読み込まれることはありません。 次のJS エラーがブラウザーコンソールのログに表示されます：*&#39;Uncaught TypeError: Cannot read property &#39;length&#39; of null at b （jstest.authorize.net/v1/AcceptCore.js:1)&#39;*）

## 原因

この問題の最も一般的な理由の1つは、Commerce AdminのAuthorize.Net設定で公開クライアントキーが指定されていないことです。

## Solution

**Authorize.net** セクションの&#x200B;**Stores** > **Settings** > **Configuration** > **Sales** > **Payment Methods**&#x200B;で、値が&#x200B;**公開クライアントキー** フィールドで指定されているかどうかを確認します。 空の場合は、Authorize.Net マーチャント アカウントからキー値を入力します。

変更を適用するには、を実行してキャッシュをクリーンアップします

```bash
bin/magento cache:clean
```
