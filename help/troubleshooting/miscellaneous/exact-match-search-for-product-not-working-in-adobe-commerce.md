---
title: Adobe Commerce 2.4.x で完全一致検索が機能しない
description: ここでは、同じ検索文字列を使用したストアフロントの検索結果が、Adobe Commerce 2.3.x とAdobe Commerce 2.4.x で異なる問題を明確に説明します。
exl-id: 0867558e-1d74-4b83-abf3-651ca7fc32cb
feature: Products, Search
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Adobe Commerce 2.4.x で完全一致検索が機能しない

ここでは、同じ検索文字列を使用したストアフロントの検索結果が、Adobe Commerce 2.3.x とAdobe Commerce 2.4.x で異なる問題を明確に説明します。

## 影響を受ける製品とバージョン

- Adobe Commerce（すべてのデプロイメント方法） 2.4.x、2.3.x
- Live Search

## 問題

<u>前提条件：</u>

属性値を持つ製品がある `Saga 1` および `Saga 16` Adobe Commerce 2.3 およびAdobe Commerce 2.4 の両方のストアで確認できます。

<u>再現手順：</u>

1. Adobe Commerce 2.3 を利用したストアの前面で、次のように入力します *佐賀 1* 検索フィールドで「」をクリックし、 **検索**.
1. 検索結果では、属性値を持つ製品のみが取得されます `Saga 1`.
1. Adobe Commerce 2.4 を利用したストアの前面で、次のように入力します *佐賀 1* 検索フィールドで「」をクリックし、 **検索**.

<u>実際の結果：</u>

2.4 での検索結果には、属性値を持つ製品が含まれます `Saga 1` および `Saga 16`.

<u>期待される結果：</u>

2.4 の検索結果は 2.3 と似ており、属性値を持つ製品のみを含みます `Saga 1`.

## 原因：

2.3.x で使用されるAdobe Commerceのネイティブ検索機能では、完全一致の検索結果が得られます。 Live Search の場合、Adobe Commerce 2.4.x でリリースされたインストール可能なオプションモジュールの実装は異なり、実際の結果は、モジュールを使用した場合に期待される動作です。

## 関連資料

[Live Search のインストール](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html) を参照してください。

[Live Search](https://devdocs.magento.com/live-search/overview.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=Live%20Search) 開発者向けドキュメントを参照してください。
