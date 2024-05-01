---
title: Fastly が有効になっているサブページにメインメニュー（カテゴリ）が表示されない
description: この記事では、Fastly または Varnish が有効になっているときに、メインメニュー（またはユーザーガイドの [ カテゴリトップナビゲーションメニュー ] （https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-top.html））がサブページのストアフロント（例：*blog/page*）に表示されない問題を修正しました。
exl-id: 7c54791d-8aa6-4f01-a28b-a7aecdb8ff74
feature: Categories, Marketing Tools
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Fastly が有効になっているサブページにメインメニュー（カテゴリ）が表示されない

この記事では、メインメニュー（または [カテゴリのトップ ナビゲーション メニュー](/docs/commerce-admin/catalog/catalog/navigation/navigation-top.html) アドビのユーザーガイドでは）がサブページ（例： *ブログ/ページ*）に設定する必要があります。

**原因：** 許可されていない `/` 文字（スラッシュ） *URL キー* ページのパラメーター（検索エンジン最適化設定）。 通常、文字は次の場合に追加されます *URL パス* （ページの場所全体を含む）が、の代わりに誤って指定されています。 *URL キー*：例： *blog/page\_name* ただ単にではなく *page\_name*.

**解決策：** を削除 `/` 文字（スラッシュ）。例： *URL キー* パラメーターで、ページ名のみを指定します。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス 2.X.X
* クラウドインフラストラクチャー 2.X.X 上のAdobe Commerce
* Fastly またはワニス

## 問題

メインメニュー（ [カテゴリのトップ ナビゲーション メニュー](/docs/commerce-admin/catalog/catalog/navigation/navigation-top.html) fastly またはその他のワニスベースのサービスが有効になっている場合、ユーザーガイドでは）がサブページのストアフロントに表示されません。

## 原因：

この問題は、許可されていないことが原因です `/` 文字（スラッシュ）、に追加 *URL キー* パラメーター（検索エンジン最適化設定）。

通常、文字は次の場合に追加されます *URL パス* （ページの親リソース/ディレクトリを含む、ページの場所全体で）が、 *URL キー*：例： *blog/page\_name* ただ単にではなく *page\_name*.

![SEO 設定用の URL キーパラメーター](assets/seo_url_key.png)

## 解決策

を削除 `/` 文字（スラッシュ）: *URL キー* ストアのすべてのページ用のパラメーター。

つまり、 *URL キー* の代わりに *URL パス*：親リソース/ディレクトリを含まないページ名のみを指定します。

### ページ階層と SEO のRecommendations

ページ階層を設定するには、 **階層** ページを編集メニューの「」セクション。

![階層設定](assets/hierarchy_hr.png)

を使用することもできます。 **コンテンツ** > **要素** > **階層** メニュー – より複雑な階層ソリューション用。

製品ページでの SEO 用には、URL リライトを使用します（**Marketing** > **SEO と検索** > **URL リライト**）に設定します。

## 詳しくは、ユーザーガイドを参照してください。

この *URL キー* seo 用のパラメーター：

* [検索エンジンの最適化](/docs/commerce-admin/catalog/categories/create/categories-search-engine-optimization.html)
* [新しいページの追加](/docs/commerce-admin/content-design/elements/pages/page-add.html)

ページ階層：

* [概要](/docs/commerce-admin/content-design/elements/pages/page-hierarchy.html)
* [ノードの追加](/docs/commerce-admin/content-design/elements/pages/page-hierarchy.html#add-a-hierarchy-node)
