---
title: Authorize.netの支払い方法が使用されている場合、チェックアウトが行き詰まる
description: ここでは、Authorize.netを使用している場合に、ブラウザーコンソールログに「Cannot read property 'length' of null」*というエラーメッセージが表示されてチェックアウトが停止するAdobe Commerce 2.3.X の問題について説明します。
exl-id: 01dc1147-4010-4dc5-81f3-3b3015a8c47c
feature: Cache, Checkout, Console, Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Authorize.netの支払い方法が使用されている場合、チェックアウトが行き詰まる

ここでは、Authorize.netを使用している場合に、ブラウザーコンソールログに「*&#39;Cannot read property &#39;length&#39; of null&#39;* というエラーメッセージが表示され、チェックアウトが行き詰まるAdobe Commerce 2.3.X の問題について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.3.X

>[!NOTE]
>
>コアとなるAdobe Commerce Authorize.Net 支払い統合は 2.3.4 以降で非推奨となり、2.4.0 で完全に削除されました。代わりに、[Adobe Commerce [!DNL Marketplace]](https://commercemarketplace.adobe.com/) のニーズに合った拡張機能を使用します。

## 問題

<u> 再現手順 </u>

1. Commerce Admin でAuthorize.net支払い方法を設定します。
1. ストアフロントに移動します。
1. 商品を買い物かごに追加し、チェックアウトに進みます。
1. 支払い方法としてAuthorize.netを選択します。
1. **Place Order** をクリックします。

<u> 期待される結果 </u>

Authorize.net iframe が読み込まれます。

<u> 実際の結果 </u>

Ajax スピナーが表示され、ページは読み込まれません。 次の JS エラーがブラウザーコンソールログに表示されます。*「Uncaught TypeError: Cannot read property &#39;length&#39; of null at b （jstest.authorize.net/v1/AcceptCore.js:1)&#39;*

## 原因：

この問題が発生する最も一般的な理由の 1 つは、Commerce管理の Authorize.Net 設定で公開クライアントキーが指定されていないことです。

## 解決策

**Stores**/**Settings**/**Configuration**/**Sales**/**Payment Methods** の下の「**Authorize.net**」セクションで、「**Public Client Key**」フィールドに値が指定されているかどうかを確認します。 空の場合は、Authorize.Net マーチャントアカウントのキー値を入力します。

変更を適用するには、次のコマンドを実行してキャッシュをクリーンアップします。

```bash
bin/magento cache:clean
```
