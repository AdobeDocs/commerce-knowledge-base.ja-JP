---
title: Google マップのすべてのAdobe Commerce バージョンのアクセス損失に対する修正パッチ
description: 「この記事では、3.54 以降の最新バージョンと互換性のないAdobe Commerce マーチャント向けに修正を提供  [!DNL Google Maps]  ます。」
feature: Install, Upgrade
role: Developer
source-git-commit: cf235c2fdd7a36d7e3b126de35c51e6711cd3845
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# すべてのAdobe Commerce バージョンの [!DNL Google Maps] アクセス損失に対する修正パッチ

この記事では、3.54 以降の最新の [!DNL Google Maps] バージョンと互換性のないAdobe Commerce マーチャント向けの修正を説明します。 この問題を修正するには、Adobe CommerceのマーチャントがAdobe Commerceのどのバージョンでも [!DNL Google Maps] にアクセスできなくなっている問題を解決します。

## 影響を受けるバージョンと製品

* Adobe Commerceまたはその他の使用済みテクノロジーのバージョン。
* Adobe Commerce *2.4.4* - *2.4.7* オンクラウドおよびオンプレミス版。

## 問題

*2024 年 6 月 14 日（PT）*[!DNL Google Maps] バージョン *3.53* は提供終了となり、[!DNL Google] 年にスイッチが切られました。

詳しくは、[[!DNL Google Maps Platform: Maps JavaScript API]](https://developers.google.com/maps/documentation/javascript/versions#documentation-for-the-api-versions) を参照してください。

Adobe Commerceは、3.54 以降の最新の [!DNL  Google Maps] バージョンとは互換性がありませんでした。

非互換性は、`lib/web/legacy-build.min.js` を通じて読み込まれた従来の `prototype.js script` がネイティブの Array.from 関数を上書きしたために発生し、[!DNL  Google Maps] API との直接競合につながります。

[[!DNL Google Maps: JS Best Practices]](https://developers.google.com/maps/documentation/javascript/best-practices) を参照。

<u> 再現手順 </u> :

1. **[!UICONTROL Content]**/**[!UICONTROL Pages]** をクリックし、**[!UICONTROL New Page]** を選択します。
1. コンテンツブロックを展開し、「**[!DNL PageBuilder]** を編集」ボタンをクリックします。
1. **[!DNL PageBuilder]** メニューからページにコンテンツブロックをマッピングをドラッグします。

<u> 期待される結果：</u>

[!DNL Google Maps] は期待どおりに動作します。

<u> 実際の結果：</u>

コンテンツをマッピング ブロック **[!DNL PageBuilder]** メニューからページにドロップすると、「*Sorry! エラーが発生しました」* 表示されます。

## 解決策

* 2.4.4、2.4.5、2.4.6 または 2.4.7 のパッチバージョンのすべてのマーチャントは、これらの対応するパッチをバージョンに適用する必要があります。

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

**注**

この問題は、8 月のセキュリティ専用パッチリリースの範囲で永続的に修正されます。
2.4.7-p2、2.4.6-p7、2.4.5-p9、2.4.4-p10

## 関連資料

[Adobeが提供する Composer パッチを適用する方法 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento)