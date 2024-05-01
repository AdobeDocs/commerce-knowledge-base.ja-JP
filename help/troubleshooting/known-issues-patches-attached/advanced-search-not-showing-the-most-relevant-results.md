---
title: 詳細検索で最も関連性の高い結果が表示されない
description: この記事では、Adobe Commerceの既知の問題に対するパッチを提供しますが、詳細検索では、最も関連性の高い結果が最初に表示されません。
exl-id: 88f0782d-ba7d-4f19-9761-7894d978d334
feature: Search
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 詳細検索で最も関連性の高い結果が表示されない

この記事では、Adobe Commerceの既知の問題に対するパッチを提供しますが、詳細検索では、最も関連性の高い結果が最初に表示されません。

## 影響を受けるバージョン {#Advancedsearchnotshowingmostrelevantresults-Affectedversions}

* Adobe Commerce（すべてのデプロイメントオプション） 2.x.x
* Magento Open Source 2.x.x

## 問題 {#Advancedsearchnotshowingmostrelevantresults-Description}

高度な検索機能では、クイック検索のように、最も関連性の高い結果が最初に返されることはありません。 問題は、選択した検索エンジンのタイプには依存しません。

<u>再現手順：</u>

1. 店頭でクイック検索に進み、「Fitted Jacket」を検索します。
1. 「Orion Two-Tone Fitted Jacket」が最初の結果であることに注意してください。
1. 詳細検索に移動し、「名前」フィールドで「Fitted Jacket」を検索します。

<u>期待される結果：</u>

「Orion Two-Tone Fitted Jacket」は、高度な検索を使用した場合の最初の結果であり、最も関連性の高い結果です。

<u>実際の結果：</u>

「Orion Two-Tone Fitted Jacket」は、最も関連性が高いものの、最初の結果ではありません。

## 解決策 {#Advancedsearchnotshowingmostrelevantresults-Solution}

この問題を解決するには、この記事に添付されているパッチを適用します。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-7256\_EE\_2.1.7\_v1.composer.patch のダウンロード](assets/MDVA-7256_EE_2.1.7_v1.composer.patch.zip)

このパッチにより、高度な検索結果に対する関連度で並べ替える実装が、デフォルトの並べ替えフィールドとして追加されます。

パッチは、影響を受けるすべてのバージョンとエディションと互換性があります。

## パッチの適用方法

手順については、を参照してください [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。

## 添付ファイル
