---
title: 2.3.4 PayPal問題のホットフィックス
description: この記事では、PayPal Express チェックアウトで地域を選択する際に注文処理中に受け取るエラーの修正について説明します。 この問題は、Adobe Commerce v2.3.4 リリースで行われた変更によって引き起こされ、PayPal Express チェックアウトのアドレスフィールドの解析方法に関連しています。
exl-id: 9f5ec100-49b0-4ac5-8951-32b5c4fe6bed
feature: Orders, Payments
role: Developer
source-git-commit: 1dcd003bd9b08741c0fba464f5520797cfaeccbb
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 2.3.4 PayPal問題のホットフィックス

この記事では、PayPal Express チェックアウトで地域を選択する際に注文処理中に受け取るエラーの修正について説明します。 この問題は、Adobe Commerce v2.3.4 リリースで行われた変更によって引き起こされ、PayPal Express チェックアウトのアドレスフィールドの解析方法に関連しています。

## 影響を受けるバージョンと製品

* Adobe Commerce on cloud infrastructure v2.3.4
* Adobe Commerce オンプレミス v2.3.4

## イシュー

PayPal Express Checkoutでの注文処理中に国と地域に入るとエラーが発生します。 この問題は、アドレスセクションの地域フィールドがテキストフィールドである国（ドロップダウンメニューではなく）であれば、どの国でも再現できます。

<u>複製する手順</u> :

1. PayPal Express チェックアウトを有効にします。
1. ゲストとして、またはログインしたときに、商品をカートに追加します。
1. 決済プロセスを見る。
1. 配送先住所を選択します。 例えば、*UK*&#x200B;を指定します。 次に、**都道府県** フィールドに入力を入力します。 例：*Nottinghamshire*。
1. 「**注文する**」ボタンをクリックして注文します。 正常な注文ページと注文確認メールが届きます。

<u>期待される結果：</u>

注文は正常に行われました。

<u>実際の結果：</u>

注文ボタンをクリックすると、次のエラーが表示されます。

```
Error 500: NOTICE: PHP message: PHP Fatal error: Uncaught Error: Call to a member
  function getId() on null in httpdocs/vendor/magento/module-paypal/Model/Api/Nvp.php:1527
```

## Solution

Adobe Commerce オンプレミスのマーチャントの場合：[magento.com](https://magento.com/tech-resources/download#download2353) ポータルの「ダウンロード」セクションから入手できる[ ホットフィックス、](https://magento.com)をマイアカウントに適用します。

Adobe Commerce on cloud infrastructureのマーチャントの場合：Adobeには、Commerce v1.0.2のCloud Patchesに修正プログラムが含まれています。最新のパッケージを適用する手順については、開発者向けドキュメントの「[Commerce リリースノートのクラウドパッチ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/release-notes/cloud-patches?itm_source=devdocs&itm_medium=quick_search&itm_campaign=federated_search&itm_term=cloud%20patche)」を参照してください。

## パッチの適用方法

手順については、サポートナレッジベースの「[Adobeが提供するコンポーザーパッチを適用する方法](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/how-to-apply-a-composer-patch-provided-by-magento)」を参照してください。

## 関連トピックス

* [ リリース情報> Adobe Commerce 2.3.4 リリースノート > Adobe Commerce 2.3.4のリージョンパッチでPayPal Expressのチェックアウトの問題を適用して、重要なPayPal Expressのチェックアウトの問題に対処します](https://commerce-docs.github.io/devdocs-archive/2.3/guides/v2.3/release-notes/release-notes-2-3-4-commerce.html#apply-the-paypal-express-checkout-issue-with-region-patch-for-magento-234-to-address-a-critical-paypal-express-checkout-issue)。詳しくは、開発者向けドキュメントを参照してください。
