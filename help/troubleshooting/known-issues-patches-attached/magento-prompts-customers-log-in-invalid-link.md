---
title: Adobe Commerceで、無効なリンクでログインすることを顧客に求める
description: この記事には、Adobe Commerce 2.3.5 の既知の問題に対するパッチへのリンクが記載されています。このパッチでは、ログインを求められますが、確認メールを再送信するリンクは機能しません。
exl-id: 8adef44f-56a6-4f57-a9b5-fb8583d8ae8d
feature: Logs
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Adobe Commerceで、無効なリンクでログインすることを顧客に求める

この記事には、Adobe Commerce 2.3.5 の既知の問題に対するパッチへのリンクが記載されています。このパッチでは、ログインを求められますが、確認メールを再送信するリンクは機能しません。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5

## 問題

Adobe Commerceでは、次のメッセージが表示されて、ログインを促すメッセージが表示されます。 *「この記事は確かではありません。 確認メールを再送信するには、ここをクリックしてください」*. この **ここをクリック** リンクは、確認リンクを送信ページを開く必要がありますが、非アクティブです。

## 解決策

この問題のパッチは、Adobe Commerce テクニカルリソースで入手できます。 [Adobe Commerce 2.3.5 のアカウント再送信確認メールのリンクに関する問題パッチ](https://magento.com/tech-resources/download?_ga=2.193540264.409362045.1590506265-807369446.1578680711#download2368). 永続的な修正は、2020 年 Q4 にリリースされるAdobe Commerce 2.3.6 で利用できるようになります。

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) composer パッチの適用方法については、を参照してください。

## 関連資料

Adobe Commerce 2.3.5 の既知の問題に関するサポートナレッジベースと開発者向けドキュメントの記事：

* [Adobe Commerce 2.3.5 の既知の問題：バーチャル製品の複数出荷注文](/help/troubleshooting/miscellaneous/magento-2-3-5-known-issue-virtual-product-multi-ship-orders.md)
* [Adobe Commerce 2.3.5 の製品比較の既知の問題](/help/troubleshooting/storefront/product-comparison-known-issue-in-magento-2-3-5.md)
* [Adobe Commerce 2.3.5、2.3.5-p1 パッチ：国の支払いの問題](/help/troubleshooting/known-issues-patches-attached/magento-2-3-5-2-3-5-p1-patch-country-payment-issue.md)
* [Adobe Commerceで、無効なリンクでログインすることを顧客に求める](/help/troubleshooting/known-issues-patches-attached/magento-prompts-customers-log-in-invalid-link.md)
* [Adobe Commerce 2.3.5 の一括アクション製品数の既知の問題](/help/troubleshooting/miscellaneous/bulk-action-product-count-known-issue-in-magento-2-3-5.md)
* [Adobe Commerce 2.3.5-p1 でのAmazon Pay チェックアウトの問題に対するパッチ](/help/troubleshooting/payments/patch-for-amazon-pay-checkout-issue-in-magento-2-3-5-p1.md)
* [Adobe Commerce 2.3.5 の既知の問題](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#known-issues)
