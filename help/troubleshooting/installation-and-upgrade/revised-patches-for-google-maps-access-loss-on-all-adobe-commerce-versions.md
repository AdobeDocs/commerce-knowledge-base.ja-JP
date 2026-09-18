---
title: すべてのAdobe Commerce バージョンでのGoogle Maps アクセス損失に対する修正されたパッチ
description: この記事では、3.54以降の最近の[!DNL Google Maps] バージョンと互換性がないAdobe Commerce マーチャントに対する修正を提供します。
feature: Install, Upgrade
role: Developer
exl-id: 6151e89a-3190-40cb-b599-94ae5530488b
source-git-commit: d7e58d6a9ed8e9b369ea41165cbdd6b362e40824
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%
---
# すべてのAdobe Commerce バージョンで[!DNL Google Maps] アクセスが失われた修正パッチ

この記事では、3.54以降の最近の[!DNL Google Maps] バージョンと互換性がないAdobe Commerce マーチャントに対する修正を提供します。 この修正は、Adobe CommerceのマーチャントがAdobe Commerceのどのバージョンでも[!DNL Google Maps]にアクセスできなくなった問題を解決するためのものです。

## 影響を受けるバージョンと製品

* Adobe Commerceやその他の使用済みテクノロジーのバージョン。
* Adobe Commerce *2.4.4* - *2.4.7* （クラウド版およびオンプレミス版）。

## イシュー

*2024年6月14日* [!DNL Google Maps] バージョン *3.53*&#x200B;が提供終了に達し、[!DNL Google]によって無効化されました。

詳しくは、[[!DNL Google Maps Platform: Maps JavaScript API]](https://developers.google.com/maps/documentation/javascript/versions#documentation-for-the-api-versions)を参照してください。

Adobe Commerceは、3.54以降の最近の[!DNL &#x200B; Google Maps] バージョンと互換性がありませんでした。

互換性がないのは、従来の`prototype.js script`が`lib/web/legacy-build.min.js`を介して読み込まれ、ネイティブのArray.from関数を上書きしたことが原因で、[!DNL &#x200B; Google Maps] APIとの直接の競合につながりました。

[[!DNL Google Maps: JS Best Practices]](https://developers.google.com/maps/documentation/javascript/best-practices)を参照してください。

<u>複製する手順</u> :

1. **[!UICONTROL Content]** > **[!UICONTROL Pages]** >をクリックし、**[!UICONTROL New Page]**&#x200B;を選択します。
1. コンテンツブロックを展開し、「**[!DNL PageBuilder]**」を編集ボタンをクリックします。
1. コンテンツブロックを&#x200B;**[!DNL PageBuilder]** メニューからページにドラッグします。

<u>期待される結果：</u>

[!DNL Google Maps]は期待どおりに機能する必要があります。

<u>実際の結果：</u>

マップ コンテンツ ブロックを&#x200B;**[!DNL PageBuilder]** メニューからページにドロップすると、*などのエラーメッセージが表示されます。「申し訳ありません。 問題が発生しました&quot;*&#x200B;が表示されます。

## Solution

* パッチバージョン 2.4.4、2.4.5、2.4.6または2.4.7のすべての販売者は、これらの対応するパッチをバージョンに適用する必要があります。

## パッチ

Adobe Commerceのバージョンに応じて、次の添付パッチを使用します。

**バージョン 2.4.4の場合：**
[ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip](assets/ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip)

**バージョン 2.4.5の場合：**
[ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip](assets/ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip)

**バージョン 2.4.6の場合：**
[ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip](assets/ACSD-60245_Google_maps_API_2.4.4_2.4.5_2.4.6_composer.patch.zip)

**バージョン 2.4.7の場合：**
[ACSD-60245_Google_maps_API_2.4.7_composer.patch.zip](assets/ACSD-60245_Google_maps_API_2.4.7_composer.patch.zip)

**ご注意ください**

この問題は、8月のセキュリティのみのパッチリリースの範囲で恒久的に修正されます。
2.4.7-p2、2.4.6-p7、2.4.5-p9、2.4.4-p10

## 関連トピックス

[Adobeが提供するコンポーザーパッチの適用方法](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento)
