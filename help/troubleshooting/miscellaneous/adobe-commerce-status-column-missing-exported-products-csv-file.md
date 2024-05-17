---
title: Adobe Commerce ステータス列に、書き出された製品の CSV ファイルが見つからない
description: この記事では、書き出された製品を含む CSV ファイルでステータス列が見つからない場合の問題の解決策を説明します。
exl-id: 3cbe1e6c-fc73-4331-add7-1ebcb28a4580
feature: Data Import/Export, Products
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Adobe Commerce ステータス列に、書き出された製品の CSV ファイルが見つからない

この記事では、書き出された製品を含む CSV ファイルでステータス列が見つからない場合（製品が有効か無効かを示す場合）の問題に対する解決策を提供します。 商品のステータスは、によって示されます [!UICONTROL product_online] 列。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法）すべて [サポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 問題

が見つかりません [!UICONTROL status] 書き出された製品を含む CSV ファイルの列 例えば、すべての SKU の CSV をステータスと共に書き出しても、テーブルに [!UICONTROL status] 列。

<u>再現手順：</u>

1. Adobe Commerce Admin で、次を選択します。 **[!UICONTROL System]**、の下 **[!UICONTROL Data Transfer]** 選択 **[!UICONTROL Export]**.
1. が含まれる **[!UICONTROL Export Settings]** セクションで、 **[!UICONTROL Entity Type]** ドロップダウン **[!UICONTROL Products]**.
1. を検索 **[!UICONTROL status]**&#x200B;の下にリストされます **[!UICONTROL Attribute Code]**. 使用可能な属性のリストに、該当する属性コードが表示されます（**[!UICONTROL Enable Product]**）に設定します。
1. クリックする **[!UICONTROL Export]**.

<u>期待される結果：</u>

書き出したばかりの CSV ファイルには、というラベルの付いた列が表示されます [!UICONTROL status].

<u>実際の結果：</u>

というラベルの付いた列は表示されません。 [!UICONTROL status] 書き出された csv ファイルで。

## 原因：

CSV ファイル内の製品のステータス属性の名前が変更されました。 現在は、 [!UICONTROL product_online] 列。

## 解決策

1. を選択 **[!UICONTROL System]**、の下 **[!UICONTROL Data Transfer]** 選択 **[!UICONTROL Import]**.
1. クリック **[!UICONTROL Download Sample File]**.
1. を確認できます [!UICONTROL product_online] 列（CSV ファイル内）。

## 関連資料

* [CSV ファイルの操作](https://docs.magento.com/user-guide/system/data-csv.html) を参照してください。
* [製品の書き出し属性リファレンス](https://docs.magento.com/user-guide/system/data-attributes-product.html) を参照してください。
