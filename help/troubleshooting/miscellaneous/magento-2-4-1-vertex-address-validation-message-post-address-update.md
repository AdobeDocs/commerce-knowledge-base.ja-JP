---
title: Adobe Commerce 2.4.1 Vertex Address の検証メッセージ後住所の更新
description: ここでは、請求先住所と異なる配送先住所を使用した場合に、支払い手順で頂点の住所の検証が機能しない、Adobe Commerce 2.4.1 の既知の問題について説明します。 この問題はAdobe Commerce 2.4.2 で修正される予定です。
exl-id: c2abeb96-e837-4d16-92dd-82fea5661dd9
feature: Shipping/Delivery
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
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

**頂点アドレス クレンジング** を有効にします。 手順については、ユーザーガイドの [ ストアフロントアドレスクレンジングの設定 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/vertex-address-cleansing-different-addresses-not-allowed.html?lang=ja) を参照してください。

<u> 再現手順：</u>

1. アカウントを作成し、ログインします。
1. **買い物かごに追加** をクリックして、買い物かごに項目を追加します。 買い物かごアイコンをクリックし、**チェックアウトに進む** をクリックします。
1. 「**発送先住所**」フィールドに有効な住所を入力します。
1. **発送方法** のオプションの 1 つをオンにします。 次に、「**次へ** をクリックします。
1. 住所検証で異なる住所情報が提示された場合は、[**住所の更新**] をクリックし、[**次へ**] をクリックします。
1. 「**請求先と配送先住所が同じです**」チェックボックスをオフにします。

<u> 最初のシナリオ：</u>

[ 上記の 6 つの手順 ](/help/troubleshooting/miscellaneous/magento-2-4-1-vertex-address-validation-message-post-address-update.md#first_sixth) に従い、次の手順を実行します。

1. 新しい有効な請求先住所を入力してください。
1. 「**更新** ボタンをクリックします。 次のようなメッセージ/提案が表示されます。*アドレスが無効です。* このメールの後に、次のようなアドレス候補が表示されます。*郵便番号：XXXXX- XXXX 通り：XXX 市区町村 XXX*
1. [**更新**] ボタンをクリックします（[ 頂点のアドレス ] 候補の [**アドレスを更新**] ボタンをクリックしないでください）。
1. 更新した請求先住所の **編集** ボタンをクリックします。
1. アドレス ドロップダウンからアドレスを選択します。
1. 「**更新** ボタンをクリックします。

<u> 期待される結果：</u>

古い検証メッセージ/提案メッセージは削除されます。

<u> 実際の結果：</u>

検証メッセージ/提案 *「有効なアドレスが見つかりませんでした。郵便番号：XXXXX-XXXX 通り：XXX 市区町村 XXX」* メッセージは **なし** 削除されました。 フォームに無効な住所を入力した場合も同じ問題が発生します。

<u>2 番目のシナリオ：</u>

[ 上記の 6 つの手順 ](/help/troubleshooting/miscellaneous/magento-2-4-1-vertex-address-validation-message-post-address-update.md#first_sixth) に従い、次の手順を実行します。

1. 住所フォームに有効な住所を入力します。
1. 「**更新** ボタンをクリックします。 次のようなメッセージ/提案が表示されます。*アドレスが無効です。* このメールの後に、次のようなアドレス候補が表示されます。*郵便番号：XXXXX-XXXX 通り：XXX 市区町村 XXX*
1. **更新** ボタンをクリックします（頂点アドレス候補の **アドレスを更新** ボタンはクリックしないでください）。
1. ***請求先と配送先住所が同じです*** ドロップダウンを確認します。

<u> 期待される結果：</u>

古い検証メッセージ/提案メッセージは削除されます。

<u> 実際の結果：</u>

検証メッセージ/提案 *「有効な住所の郵便番号：XXXXX-XXXX Street XXX City street XXX」* メッセージが **なし** 削除されました。 フォームに無効な住所を入力した場合も同じ問題が発生します。

## サポートナレッジベースの関連資料：

[Adobe Commerce 2.3.6、2.4.0-p1 および 2.4.1 既知の問題：アカウントが有効な場合、dotdigital にログインできない](/help/troubleshooting/miscellaneous/magento-2-3-6-2-4-0-p1-2-4-1-known-issue-dotdigital-login.md)
