---
title: ファイルストレージが少なく、特定のページの読み込みが遅い
description: この記事では、画像が大きくリッチになることでディスク領域が小さくなる問題の解決策について説明します。
exl-id: 640c8f0d-f714-4cc1-a401-9264cfaf8e37
feature: Storage, Observability
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# ファイルストレージが少なく、特定のページの読み込みが遅い

この記事では、画像が大きくリッチになることでディスク領域が小さくなる問題の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce（サポート対象のすべてのバージョン）
* Adobe Commerce オンプレミス、サポートされているすべてのバージョン
* Magento Open Source、サポートされているすべてのバージョン

## 問題

大容量の画像がで大量のストレージを使用していると、ディスクのストレージが少なくなり、ページの読み込みに時間がかかる可能性があります。 `pub/media/catalog/products` （専用のステージング環境がプロビジョニングされていない限り）ステージング環境と実稼動環境の間でディスク領域を共有する。

## 原因：

パフォーマンスと表示品質のバランスを取るために画像が最適化されていない。

## 解決策

画像をアップロードする前に、パフォーマンスと表示品質のバランスを取るために画像を最適化および圧縮します。 これにより、スペースを増やし、ページ読み込み時間を短縮できます。 PNG は、単色の領域が大きい画像ほどサイズが小さくなります。 JPEGは他のすべてのもののために小さいサイズを与えます。 最も高い圧縮率を使用します（著しい劣化は発生しません）。 これは通常 60～80% です。

使用方法 [Fastly 画像の最適化](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization.html) より記憶効率の良い画像を生成する。

## 関連資料

ディスク容量の管理について（クラウドインフラストラクチャ上のAdobe Commerceを使用している場合）詳しくは、 [Adobe Commerceでのディスク容量の管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html) （Commerce on Cloud Infrastructure ガイド）を参照してください。
