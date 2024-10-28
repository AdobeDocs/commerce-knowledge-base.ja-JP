---
title: Adobe Commerce 2.3.5 の製品比較の既知の問題
description: この記事では、Adobe Commerce オンプレミス 2.3.5 およびAdobe Commerce on cloud infrastructure 2.3.5 における既知の [product comparison] （https://docs.magento.com/user-guide/marketing/product-compare.html）の問題を回避する方法について推奨事項を説明します。
exl-id: 1488e2db-4a5d-4963-b48e-b84f760582d1
feature: Products, Storefront
role: Admin
source-git-commit: d51fd4d7b064b8eea6cd3771af279b74a8bdec48
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Adobe Commerce 2.3.5 の製品比較の既知の問題

この記事では、Adobe Commerce オンプレミス 2.3.5 およびAdobe Commerce on cloud infrastructure 2.3.5 の既知の [ 製品比較 ](https://docs.magento.com/user-guide/marketing/product-compare.html) 問題を回避する方法に関する推奨事項を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.3.5
* クラウドインフラストラクチャー 2.3.5 上のAdobe Commerce

## 問題

ユーザーが様々なストアビューの商品を比較しようとしたときに、ある商品の同等の属性に空の値が含まれている場合、Adobe Commerceに破損した「商品の比較」ページが表示されます。

## 解決策

同等の製品属性に空でない値を指定するか、属性にデフォルトのストア表示値を使用します。 比較可能な属性値は空にできません。

>[!NOTE]
>
>製品属性は、「ストアフロントで比較 **設定を使用した比較に使用されるように** 定されています。 詳しくは、製品ユーザーガイドの [ 製品属性の作成 ](https://docs.magento.com/user-guide/stores/attribute-product-create.html#step-4-describe-the-storefront-properties) を参照してください。

修正は、2020 年 Q4 にリリースされるAdobe Commerce 2.3.6 で利用できるようになります。

この修正は GitHub で確認できます（この修正は回帰テストを経ておらず、公式のホットフィックスではないことを考慮してください）。<https://github.com/magento/magento2/pull/27662>

## 関連資料

<ul><li>Adobe Commerce 2.3.5 の既知の問題に関するAdobe Commerce サポートナレッジベースの記事：<ul>
<li>
<p title="Adobe Commerce 2.3.5 でバーチャル商品が正しく処理されない複数出荷の注文"><a href="/help/troubleshooting/miscellaneous/magento-2-3-5-known-issue-virtual-product-multi-ship-orders.md">Adobe Commerce 2.3.5 でバーチャル商品が正しく処理されない複数出荷の注文</a></p>
</li>
<li><a href="/help/troubleshooting/miscellaneous/bulk-action-product-count-known-issue-in-magento-2-3-5.md">Adobe Commerce 2.3.5 の一括アクション製品数の既知の問題</a></li>
<li>
<p title="Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.5 および 2.3.5-p1 における国の支払い方法の問題"><a href="/help/troubleshooting/known-issues-patches-attached/magento-2-3-5-2-3-5-p1-patch-country-payment-issue.md">Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.5 および 2.3.5-p1 における国の支払い方法の問題</a></p>
</li>
<li>
<p title="Adobe Commerce 2.3.5-p1 でのAmazon Pay チェックアウトの問題に対するパッチ"><a href="/help/troubleshooting/payments/patch-for-amazon-pay-checkout-issue-in-magento-2-3-5-p1.md">Adobe Commerce 2.3.5-p1 でのAmazon Pay チェックアウトの問題に対するパッチ</a></p>
</li>
</ul>
</li><li><a href="https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#known-issues">Adobe Commerce 2.3.5 の既知の問題 </a> については、開発者向けドキュメントを参照してください。</li></ul>
