---
title: Adobe Commerce 2.4.1 Vertex Address の検証メッセージ後住所の更新
description: ここでは、請求先住所と異なる配送先住所を使用した場合に、支払い手順で頂点の住所の検証が機能しない、Adobe Commerce 2.4.1 の既知の問題について説明します。 この問題はAdobe Commerce 2.4.2 で修正される予定です。
exl-id: c2abeb96-e837-4d16-92dd-82fea5661dd9
feature: Shipping/Delivery
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Adobe Commerce 2.4.1 Vertex Address の検証メッセージ後住所の更新

ここでは、請求先住所と異なる配送先住所を使用した場合に、支払い手順で頂点の住所の検証が機能しない、Adobe Commerce 2.4.1 の既知の問題について説明します。 この問題はAdobe Commerce 2.4.2 で修正される予定です。

## 影響を受ける製品とバージョン

* Vertex 統合が有効なAdobe Commerce オンプレミス 2.4.1
* Vertex 統合を有効にしたクラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

## 問題

前提条件：

Enable （有効） **頂点アドレス クレンジング**. 手順については、次を参照してください [ストアフロントアドレスのクレンジングの設定](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/vertex-address-cleansing-different-addresses-not-allowed.html) を参照してください。

<u>再現手順：</u>

1. アカウントを作成し、ログインします。
1. をクリックして、買い物かごに項目を追加する **カートに追加**. 買い物かごアイコンをクリックし、 **チェックアウトに進む**.
1. に有効なアドレスを入力 **発送先住所** フィールド。
1. 次のいずれかのオプションをオンにします **発送方法**. 次に、 **次**.
1. 住所の検証で別の住所情報が提示された場合は、 **アドレスを更新** をクリックして、 **次**.
1. 「」をオフにします **請求先と配送先住所が同じです** チェックボックス。

<u>最初のシナリオ：</u>

に従う [6 段階以上](/help/troubleshooting/miscellaneous/magento-2-4-1-vertex-address-validation-message-post-address-update.md#first_sixth) その後：

1. 新しい有効な請求先住所を入力してください。
1. 「」をクリック **更新** ボタン。 次のようなメッセージ/提案が表示されます。 *アドレスが無効です。* その後、次のようなアドレス候補が表示されます。 *郵便番号：XXXXX- XXXX 番地：XXX 市区町村 XXX*
1. 「」をクリック **更新** ボタン（ **アドレスを更新** 頂点アドレス候補のボタン）。
1. 「」をクリック **編集** 更新された請求先住所のボタン。
1. アドレス ドロップダウンからアドレスを選択します。
1. 「」をクリック **更新** ボタン。

<u>期待される結果：</u>

古い検証メッセージ/提案メッセージは削除されます。

<u>実際の結果：</u>

検証メッセージ /提案 *「有効な住所 Postcode : XXXXX-XXXX Street : XXX City street XXX が見つかりませんでした」* メッセージは **ではない** を削除しました。 フォームに無効な住所を入力した場合も同じ問題が発生します。

<u>2 番目のシナリオ：</u>

に従う [6 段階以上](/help/troubleshooting/miscellaneous/magento-2-4-1-vertex-address-validation-message-post-address-update.md#first_sixth) その後：

1. 住所フォームに有効な住所を入力します。
1. 「」をクリック **更新** ボタン。 次のようなメッセージ/提案が表示されます。 *アドレスが無効です。* その後、次のようなアドレス候補が表示されます。 *郵便番号：XXXXX-XXXX 番地：XXX 市区町村 XXX*.
1. 「」をクリック **更新** ボタン（ **アドレスを更新** 頂点アドレス候補のボタン）。
1. を確認します ***請求先と配送先住所が同じです*** ドロップダウン。

<u>期待される結果：</u>

古い検証メッセージ/提案メッセージは削除されます。

<u>実際の結果：</u>

検証メッセージ /提案 *「有効な郵便番号：XXXXX-XXXX Street XXX City street XXX が見つかりませんでした」* メッセージは **ではない** を削除しました。 フォームに無効な住所を入力した場合も同じ問題が発生します。

## サポートナレッジベースの関連資料：

[Adobe Commerce 2.3.6、2.4.0-p1 および 2.4.1 既知の問題：アカウントが有効な場合、dotdigital にログインできない](/help/troubleshooting/miscellaneous/magento-2-3-6-2-4-0-p1-2-4-1-known-issue-dotdigital-login.md)
