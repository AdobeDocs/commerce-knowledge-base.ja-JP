---
title: 「Adobe Commerce 2.4.0：顧客のアクティビティの更新が機能しない」
description: この記事では、管理者ユーザーが顧客の注文を作成し、顧客のアクティビティ サイドパネルの「更新」ボタンが機能しない場合の、Adobe Commerce 2.4.0 の既知の問題の解決策を説明します。
exl-id: 50048e9f-6009-4db5-ae4a-c35a84cec265
feature: Configuration
role: Developer
source-git-commit: a1046621259ea49eab74cd6ba3bba550e0c70283
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Adobe Commerce 2.4.0：顧客のアクティビティの更新が機能しない

この記事では、管理者ユーザーが顧客の注文を作成し、顧客のアクティビティ サイドパネルの「更新」ボタンが機能しない場合の、Adobe Commerce 2.4.0 の既知の問題の解決策を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

## 問題

<u> 再現手順 </u>:

1. **管理パネル**/**営業**/**注文** に移動します。
1. 「**新しい注文を作成** ボタンをクリックします。
1. 作成した顧客を選択します。
1. 作成した顧客としてストアフロントに移動します。
1. **製品** ページに移動します。 **顧客のアクティビティ** の **最近表示された製品** セクションの **更新** ボタンをクリックします。
1. ストアフロントに戻ります。
1. 作成した製品を使用して注文します。
1. **管理パネル** に戻り、「顧客のアクティビティ **の** 最終注文項目 **セクションの**&#x200B;**更新** ボタンをクリックします。
1. ストアフロントに戻ります。 作成した製品を **比較リスト** に追加します。
1. **管理パネル** に戻ります。 **顧客のアクティビティ** の **比較リストの製品** セクションの **更新** ボタンをクリックします。
1. ストアフロントに戻ります。
1. 作成した製品を **比較リスト** から削除します。
1. **管理パネル** に戻ります。
1. **顧客のアクティビティ** の **最近比較した製品** セクションの **更新** ボタンをクリックします。
1. ストアフロントに戻ります。

<u> 期待される結果 </u>:

製品の名前は、「**最近表示された製品**」、「**最後に注文された項目**」、「**比較リストの製品**」および「**最近比較された製品**」セクションに表示される必要があります。

<u> 実際の結果 </u>:

「**更新** ボタンがクリックされるたびに、ページが上にスクロールされます。 製品の名前が適切なセクションに表示されません。

## 解決策

これを回避するには、管理者ユーザーが、サイドバーの下部にある **変更を更新** ボタンをクリックして **顧客のアクティビティ** を更新します。 この問題は、Adobe Commerce 2.4.1 パッチで解決される予定です。

![mceclip0.png](assets/mceclip0.png)

## 関連資料

* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintree支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 の既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
