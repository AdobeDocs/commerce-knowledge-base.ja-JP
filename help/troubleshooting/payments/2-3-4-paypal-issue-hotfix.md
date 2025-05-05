---
title: 2.3.4 PayPal 問題のホットフィックス
description: この記事では、PayPal Express Checkout でリージョンを選択する際に、注文の発注中に発生したエラーを修正します。 この問題は、Adobe Commerce v2.3.4 リリースで行われた変更によって発生し、PayPal Express のチェックアウトアドレスフィールドの解析方法に関連しています。
exl-id: 9f5ec100-49b0-4ac5-8951-32b5c4fe6bed
feature: Orders, Payments
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# 2.3.4 PayPal 問題のホットフィックス

この記事では、PayPal Express Checkout でリージョンを選択する際に、注文の発注中に発生したエラーを修正します。 この問題は、Adobe Commerce v2.3.4 リリースで行われた変更によって発生し、PayPal Express のチェックアウトアドレスフィールドの解析方法に関連しています。

## 影響を受けるバージョンと製品

* クラウドインフラストラクチャー上のAdobe Commerce v2.3.4
* Adobe Commerce オンプレミス v2.3.4

## 問題

PayPal Express Checkout で注文を発注する際に、国と地域を入力するとエラーが発生します。 この問題は、アドレスセクションの地域フィールドがテキストフィールド（ドロップダウンメニューとは異なる）である国でも再現できます。

<u> 再現手順 </u> :

1. PayPal Express チェックアウトを有効にします。
1. 製品をゲストとして、またはログイン中に買い物かごに追加します。
1. チェックアウトに移動します。
1. 配送先住所を選択します。 例えば、*UK* です。 次に、「**都道府県** フィールドに入力を入力します。 例えば、*Nottinghamshire* などです。
1. 「**注文する**」ボタンをクリックして注文します。 注文ページと注文確認メールが正常に送信されます。

<u> 期待される結果：</u>

注文が正常に完了しました。

<u> 実際の結果：</u>

注文ボタンをクリックすると、次のエラーが表示されます。

```
Error 500: NOTICE: PHP message: PHP Fatal error: Uncaught Error: Call to a member
  function getId() on null in httpdocs/vendor/magento/module-paypal/Model/Api/Nvp.php:1527
```

## 解決策

Adobe Commerce オンプレミスのマーチャントの場合：[magento.com](https://magento.com/tech-resources/download#download2353) ポータルの「ダウンロード」セクションにある [ ホットフィックス ](https://magento.com) をマイアカウントで適用します。

クラウドインフラストラクチャマーチャント上のAdobe Commerceの場合：Adobeでは、Commerce v1.0.2 のクラウドパッチの修正が含まれています。最新のパッケージを適用する手順については、開発者向けドキュメントの [Commerce リリースノートのクラウドパッチ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/release-notes/cloud-patches?itm_source=devdocs&amp;itm_medium=quick_search&amp;itm_campaign=federated_search&amp;itm_term=cloud%20patche) を参照してください。

## パッチの適用方法

手順については、サポートナレッジベースの [Adobe提供の Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 関連資料

* [ リリース情報 > Adobe Commerce 2.3.4 リリースノート > Adobe Commerce 2.3.4 のリージョンパッチで PayPal Express Checkout の問題を適用して、開発者向けドキュメントの重要な PayPal Express Checkout の問題に対処してください ](https://commerce-docs.github.io/devdocs-archive/2.3/guides/v2.3/release-notes/release-notes-2-3-4-commerce.html#apply-the-paypal-express-checkout-issue-with-region-patch-for-magento-234-to-address-a-critical-paypal-express-checkout-issue)。
