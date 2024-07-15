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

専用のステージング環境がプロビジョニングされていない限り、ス `pub/media/catalog/products` ージングに大量のストレージを使用し、ステージングと実稼動環境の間でディスク領域を共有すると、大きなリッチ画像が原因で、ディスク記憶域が少なくページの読み込みが遅くなる可能性があります。

## 原因：

パフォーマンスと表示品質のバランスを取るために画像が最適化されていない。

## 解決策

画像をアップロードする前に、パフォーマンスと表示品質のバランスを取るために画像を最適化および圧縮します。 これにより、スペースを増やし、ページ読み込み時間を短縮できます。 PNG は、単色の領域が大きい画像ほどサイズが小さくなります。 JPEGは他のすべてのもののために小さいサイズを与えます。 最も高い圧縮率を使用します（著しい劣化は発生しません）。 これは通常 60～80% です。

[Fastly 画像の最適化 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization.html) を使用すると、よりストレージ効率の高い画像を作成できます。

## 関連資料

Commerce on Cloud Infrastructure を使用している場合のディスク容量の管理については、Adobe Commerce on Cloud Infrastructure ガイドの [Adobe Commerceでのディスク容量の管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html) を参照してください。
