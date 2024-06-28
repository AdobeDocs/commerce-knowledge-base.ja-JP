---
title: Google マップのすべてのAdobe Commerce バージョンのアクセス損失に対する修正パッチ
description: 「この記事では、最近使用したものとは互換性のないAdobe Commerce マーチャント向けに修正を提供します [!DNL Google Maps] 3.54 以降のバージョン。'
feature: Install, Upgrade
role: Developer
source-git-commit: 49bc0b643c10c6597d6a905935c36251e92b18f9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# のパッチの改訂 [!DNL Google Maps] すべてのAdobe Commerce バージョンのアクセスが失われる

この記事では、最近のバージョンと互換性のないAdobe Commerce マーチャント向けに修正を提供します [!DNL Google Maps] 3.54 以降のバージョン この修正は、Adobe Commerceのマーチャントがにアクセスできない問題を解決するためです [!DNL Google Maps] （Adobe Commerceの任意のバージョンで既にサポートされています）。

## 影響を受けるバージョンと製品

* Adobe Commerceまたはその他の使用済みテクノロジーのバージョン。
* Adobe Commerce *2.4.4* - *2.4.7* オンクラウドおよびオンプレミスのバージョン。

## 問題

日付： *2024 年 6 月 14 日（Pt）* [!DNL Google Maps] version *3.53* 寿命に達し、によりオフにされました [!DNL Google].

詳しくは、[[!DNL Google Maps] プラットフォーム：JavaScript API] （https://developers.google.com/maps/documentation/javascript/versions#documentation-for-the-api-versions）をマッピングします。

Adobe Commerceは、最近のと互換性がありませんでした [!DNL  Google Maps] 3.54 以降のバージョン

非互換性はレガシーが原因でした `prototype.js script`を介して読み込まれます `lib/web/legacy-build.min.js` ネイティブの Array.from 関数をオーバーライドします。これにより、と直接競合します。 [!DNL  Google Maps] API です。

[[!DNL Google Maps: JS Best Practices]] （https://developers.google.com/maps/documentation/javascript/best-practices）。

<u>再現手順</u> :

1. に移動 **[!UICONTROL Content]** > **[!UICONTROL Pages]** > をクリックし、 **[!UICONTROL New Page]**.
1. コンテンツブロックを展開し、編集をクリックします。 **[!DNL PageBuilder]** ボタン。
1. 「コンテンツをマップ」ブロックを **[!DNL PageBuilder]** メニューからページ。

<u>期待される結果：</u>

[!DNL Google Maps] は期待どおりに動作します。

<u> 実際の結果：</u>

マップコンテンツブロックを次からドロップする場合： **[!DNL PageBuilder]** ページへのメニュー、エラーメッセージ（例：） *「ごめんなさい！ 問題が発生しました」* が表示されます。

## 解決策

* 2.4.4、2.4.5、2.4.6 または 2.2.7 のパッチバージョンのすべてのマーチャントは、これらの対応するパッチをバージョンに適用する必要があります。

## パッチ

Adobe Commerceのバージョンに応じて、次のパッチを適用します。

**バージョン 2.4.4 の場合：**
[ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip](assets/ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip)

**バージョン 2.4.5 の場合：**
[ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip](assets/ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip)

**バージョン 2.4.6 の場合：**
[ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip](assets/ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip)

**バージョン 2.4.7 の場合：**
[ACSD-60245_Google_maps_API_2.4.7_composer.patch.zip](assets/ACSD-60245_Google_maps_API_2.4.7_composer.patch.zip)

**注意してください**

この問題は、8 月のセキュリティ専用パッチリリース（2.4.7-p2、2.4.6-p7、2.4.5-p9、2.4.4-p10）の範囲で永続的に修正されます

## 関連資料

[Adobeが提供する composer パッチの適用方法](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento)