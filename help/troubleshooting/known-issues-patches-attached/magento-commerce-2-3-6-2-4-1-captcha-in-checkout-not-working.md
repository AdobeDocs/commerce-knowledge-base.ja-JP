---
title: Adobe Commerce 2.3.6、2.4.1 チェックアウト時の CAPTCHA が機能しない
description: この記事では、Adobe Commerceで Paypal Express、Payflow Pro、CyberSource などのサードパーティの支払いプロバイダーを使用している場合に、チェックアウトの CAPTCHA 機能が Place Order ページで期待どおりに動作しない問題に対するパッチを提供します。
exl-id: 46ab7f4d-ee0a-4cc1-96cc-6eb408319e9c
feature: Checkout, Orders
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# Adobe Commerce 2.3.6、2.4.1 チェックアウト時の CAPTCHA が機能しない

この記事では、Adobe Commerceで Paypal Express、Payflow Pro、CyberSource などのサードパーティの支払いプロバイダーを使用している場合に、チェックアウトの CAPTCHA 機能が Place Order ページで期待どおりに動作しない問題に対するパッチを提供します。

この既知の問題については、開発者向けドキュメントに記載されています。

<u>Adobe Commerce 2.3.6 の場合 </u>:

* [Adobe Commerce 2.3.6 リリースノート：既知の問題 ](https://devdocs.magento.com/guides/v2.3/release-notes/commerce-2-3-6.html#known-issues)
* [Magento Open Source 2.3.6 リリースノート：既知の問題 ](https://devdocs.magento.com/guides/v2.3/release-notes/open-source-2-3-6.html#known-issues)

<u>Adobe Commerce 2.4.1 の場合 </u>:

* [Adobe Commerce 2.4.1 リリースノート：既知の問題 ](https://devdocs.magento.com/guides/v2.4/release-notes/commerce-2-4-1.html#known-issues)
* [Magento Open Source 2.4.1 リリースノート：既知の問題 ](https://devdocs.magento.com/guides/v2.4/release-notes/open-source-2-4-1.html#known-issues)

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.3.6 および 2.4.1
* Magento Open Source 2.3.6 および 2.4.1

## 問題

<u> 再現手順 </u>

1. Commerceで、Paypal Express、Paypflow Pro、CyberSource のいずれかの支払い方法を少なくとも 1 つ設定します。
1. **管理者/ ストア /設定/顧客/顧客設定/ CAPTCHA** に移動します。
   * **ストアフロントで CAPTCHA を有効にする**= *はい* を設定します。
   * **Forms** : *チェックアウト/注文*、*ログイン*、*パスワードを忘れた場合* を選択します。
   * **表示モード** = *ログイン試行回数後* を設定します（**ログイン失敗回数** 設定を表示します）。
   * **ログインに失敗した回数** = *0* を設定します（captcha を常に機能させる場合）。
1. フロントエンドで、買い物かごに製品を追加し、チェックアウトを試みます。
1. 支払い情報ページに captcha と入力し、Paypal Express、Payflow Pro、または CyberSource でチェックアウトしてみてください。

<u> 期待される結果：</u>

CAPTCHA 機能は、期待どおりに機能します。

<u> 実際の結果：</u>

「*CAPTCHA コードを指定し、再試行してください。*」というエラーメッセージが表示されます。

## 解決策

Adobe Commerce オンプレミス/Adobe Commerce on cloud infrastructure/Magento Open Source 2.3.6 と 2.4.1 のどちらに属しているかに応じて、以下のいずれかのパッチを適用します。

## パッチ

パッチはこの記事に添付されており、`.composer` 形式と `.git` 形式の両方でダウンロードできます。

パッチをダウンロードするには、記事の最後までスクロールしてファイル名をクリックするか、次のいずれかのリンクをクリックします。

<u>Adobe Commerce オンプレミス/Adobe Commerce on cloud infrastructure/Magento Open Source 2.3.6 の場合 </u> :

* [Composer パッチ MDVA-33093\_\_\_\_2\_3\_x-p1\_\_CAPTCHA\_COMPOSER.patch](assets/MDVA-33093____2_3_x-p1__CAPTCHA_COMPOSER.patch.zip)
* [Git パッチ MDVA-33093\_\_\_\_2\_3\_x-p1\_\_CAPTCHA\_GIT.patch](assets/MDVA-33093____2_3_x-p1__CAPTCHA_GIT.patch.zip)

<u>Adobe Commerce オンプレミス/Adobe Commerce on cloud infrastructure/Magento Open Source 2.4.1 の場合 </u> :

* [Composer パッチ MDVA-33093\_\_\_\_2\_4\_x-p1\_\_CAPTCHA\_COMPOSER.patch](assets/MDVA-33093____2_4_x-p1__CAPTCHA_COMPOSER.patch.zip)
* [Git パッチ MDVA-33093\_\_\_\_2\_4\_x-p1\_\_CAPTCHA\_GIT.patch](assets/MDVA-33093____2_4_x-p1__CAPTCHA_GIT.patch.zip)

これらのパッチは、他のAdobe CommerceまたはMagento Open Sourceのバージョンやエディションとは互換性がありません。

## パッチの適用方法

<u>Composer パッチ </u>

Composer パッチの手順については、サポート技術情報の [Adobe提供の Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

<u>Git パッチ </u>

Adobe Commerce/Magento Open Sourceの Git パッチ手順については、開発者向けドキュメント [ パッチの適用：カスタムパッチ ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#custom-patches) を参照してください。
