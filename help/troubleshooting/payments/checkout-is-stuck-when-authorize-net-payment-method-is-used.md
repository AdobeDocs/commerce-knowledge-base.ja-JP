---
title: Authorize.netの支払い方法が使用されている場合、チェックアウトが行き詰まる
description: ここでは、Authorize.netを使用している場合に、ブラウザーコンソールログに「Cannot read property 'length' of null」*というエラーメッセージが表示されてチェックアウトが停止するAdobe Commerce 2.3.X の問題について説明します。
exl-id: 01dc1147-4010-4dc5-81f3-3b3015a8c47c
feature: Cache, Checkout, Console, Orders, Payments
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Authorize.netの支払い方法が使用されている場合、チェックアウトが行き詰まる

この記事では、Authorize.netを使用するとチェックアウトが行き詰まるAdobe Commerce 2.3.X の問題（ *「null のプロパティ「length」を読み取れません」* ブラウザーコンソールログにエラーメッセージが表示されます。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.3.X

>[!NOTE]
>
>コアとなるAdobe Commerce Authorize.Net 支払い統合は 2.3.4 以降で非推奨となり、2.4.0 で完全に削除されました。のニーズに合った拡張機能を使用する [Adobe Commerce [!DNL Marketplace]](https://commercemarketplace.adobe.com/) その代わり。

## 問題

<u>再現手順</u>

1. Commerce Admin でAuthorize.net支払い方法を設定します。
1. ストアフロントに移動します。
1. 商品を買い物かごに追加し、チェックアウトに進みます。
1. 支払い方法としてAuthorize.netを選択します。
1. クリック **注文する**.

<u>期待される結果</u>

Authorize.net iframe が読み込まれます。

<u>実際の結果</u>

Ajax スピナーが表示され、ページは読み込まれません。 次の JS エラーがブラウザーコンソールログに表示されます。 *「キャッチされない TypeError: b で null のプロパティ「length」を読み取れません（jstest.authorize.net/v1/AcceptCore.js:1)&#39;*

## 原因：

この問題が発生する最も一般的な理由の 1 つは、Commerce管理の Authorize.Net 設定で公開クライアントキーが指定されていないことです。

## 解決策

次の下 **ストア** > **設定** > **設定** > **売上** > **支払い方法**、内 **Authorize.net** セクションで、値がで指定されているかどうかを確認する **公開クライアントキー** フィールド。 空の場合は、Authorize.Net マーチャントアカウントのキー値を入力します。

変更を適用するには、次のコマンドを実行してキャッシュをクリーンアップします。

```bash
bin/magento cache:clean
```
