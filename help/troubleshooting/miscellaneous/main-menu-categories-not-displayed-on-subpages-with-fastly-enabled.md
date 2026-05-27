---
title: Fastlyが有効になっているサブページにメインメニュー（カテゴリー）が表示されない
description: この記事では、FastlyまたはVarnishが有効になっている場合に、メインメニュー（またはユーザーガイドの[ カテゴリトップナビゲーションメニュー] （https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-top.html））がサブページ（*blog/page*など）のストアフロントに表示されない場合の修正点を説明します。
exl-id: 7c54791d-8aa6-4f01-a28b-a7aecdb8ff74
feature: Categories, Marketing Tools
role: Developer
source-git-commit: 724a30310c3841f8280628436925f9a3e5933b14
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Fastlyが有効になっているサブページにメインメニュー（カテゴリー）が表示されない

この記事では、FastlyまたはVarnishが有効になっている場合に、メインメニュー（またはユーザーガイドの[&#x200B; カテゴリトップナビゲーションメニュー](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-top.html)）がサブページ（*ブログ/ページ*&#x200B;など）のストアフロントに表示されない場合の修正を説明します。

**原因：** ページの&#x200B;*URL キー* パラメーターの許可されていない`/`文字（スラッシュ）（検索エンジン最適化設定）。 文字は通常、*URL キー*&#x200B;ではなく&#x200B;*URL パス* （ページ全体の場所を含む）が誤って指定された場合に追加されます。例えば、*ページ\_name*&#x200B;ではなく&#x200B;*ブログ/ページ\_name*。

**解決策：** `/`文字（スラッシュ）を削除します。*URL キー* パラメーターの場合は、ページ名のみを指定します。

## 影響のあるバージョン

* Adobe Commerce オンプレミス 2.X.X
* Adobe Commerce on cloud infrastructure 2.X.X
* FastlyまたはVarnish

## イシュー

Fastlyまたはその他のVarnish ベースのサービスが有効になっている場合、メインメニュー（ユーザーガイドでは[&#x200B; カテゴリトップナビゲーションメニュー](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-top.html)とも呼ばれます）がサブページのストアフロントに表示されません。

## 原因

この問題は、許可されていない`/`文字（スラッシュ）が&#x200B;*URL キー* パラメーター（検索エンジン最適化設定）に追加されたことが原因で発生します。

文字は通常、*URL キー*&#x200B;ではなく、*URL パス* （ページの親リソース/ディレクトリを含むページ全体）が誤って指定された場合に追加されます。例えば、*ページ\_name*&#x200B;ではなく&#x200B;*ブログ/ページ\_name*。

![SEO設定のURL キーパラメーター](assets/seo_url_key.png)

## Solution

ストアのすべてのページの&#x200B;*URL キー* パラメーターから`/`文字（スラッシュ）を削除します。

つまり、*URL パス*&#x200B;の代わりに&#x200B;*URL キー*&#x200B;を使用します。親リソースやディレクトリがないページ名だけを指定します。

### ページ階層とSEOに関する推奨事項

ページ階層を設定するには、ページを編集メニューの「**階層**」セクションを使用します。

![階層設定](assets/hierarchy_hr.png)

より複雑な階層ソリューションの場合は、**コンテンツ** > **要素** > **階層** メニューを使用することもできます。

商品ページのSEO目的では、URLの書き換え（**マーケティング** > **SEOと検索** > **URLの書き換え**）を使用します。

## 詳しくは、アドビのユーザーガイドをご覧ください

SEOの&#x200B;*URL キー* パラメーター：

* [検索エンジン最適化](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-search-engine-optimization.html)
* [新しいページの追加](https://experienceleague.adobe.com/docs/commerce-admin/content-design/elements/pages/page-add.html)

ページ階層：

* [概要](https://experienceleague.adobe.com/docs/commerce-admin/content-design/elements/pages/page-hierarchy.html)
* [ノードの追加](https://experienceleague.adobe.com/docs/commerce-admin/content-design/elements/pages/page-hierarchy.html#add-a-hierarchy-node)
