---
title: バンドルオプションの順序が読み込みで更新されない
description: この記事では、.csv ファイルから製品を読み込んだ後、バンドル製品オプションが読み込みファイルでリストされている順序とは異なる順序で表示される場合の問題の解決策を説明します。
exl-id: 7f7bf782-4b35-4067-aa94-417097079f1f
feature: Data Import/Export
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# バンドルオプションの順序が読み込みで更新されない

この記事では、.csv ファイルから製品を読み込んだ後、バンドル製品オプションが読み込みファイルでリストされている順序とは異なる順序で表示される場合の問題の解決策を説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x
* Adobe Commerce オンプレミス 2.2.x、2.3.x
* Magento Open Source

## 問題

<u> 前提条件 </u>:

バンドル製品を含む有効な.csv ファイルがある。

<u> 再現手順 </u>:

1. [&#x200B; インポート機能 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/import/data-import) を使用してファイルをインポートします。
1. バンドル製品ページを開きます。

<u> 期待される結果 </u>:

オプションの順序は、.csv ファイルの場合と同じです。

<u> 実際の結果 </u>:

オプションの順序は、.csv ファイルの順序とは異なります。

## 原因：

オプションの位置が明示的に宣言されませんでした。

## 解決策

1. .csv ファイル内の `bundle_values` 列の `position` パラメーターで、各オプションに対して位置を明示的に宣言します。 詳しい手順については、製品ガイドの [&#x200B; 製品データの編集 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/examples/data-transfer-bundle-products#method-2-edit-the-product-data) を参照してください。
1. 読み込み操作を繰り返します。

読み込みの一般情報については、ユーザーガイドの [&#x200B; バンドル製品の読み込み &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/examples/data-transfer-bundle-products) を参照してください。
