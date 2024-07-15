---
title: Adobe Commerce ステータス列に、書き出された製品の CSV ファイルが見つからない
description: この記事では、書き出された製品を含む CSV ファイルでステータス列が見つからない場合の問題の解決策を説明します。
exl-id: 3cbe1e6c-fc73-4331-add7-1ebcb28a4580
feature: Data Import/Export, Products
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Adobe Commerce ステータス列に、書き出された製品の CSV ファイルが見つからない

この記事では、書き出された製品を含む CSV ファイルでステータス列が見つからない場合（製品が有効か無効かを示す場合）の問題に対する解決策を提供します。 製品のステータスは、[!UICONTROL product_online] の列に示されます。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法）すべてのバージョン [ サポートされているバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 問題

書き出された製品を含む CSV ファイルで [!UICONTROL status] 列が見つかりません。 例えば、ステータスを含むすべての SKU の CSV を書き出しても、テーブルには [!UICONTROL status] 列が表示されない場合があります。

<u> 再現手順：</u>

1. Adobe Commerce管理者で「**[!UICONTROL System]**」を選択し、「**[!UICONTROL Export]**」 **[!UICONTROL Data Transfer]** 選択します。
1. 「**[!UICONTROL Export Settings]**」セクションで、「**[!UICONTROL Entity Type]**」ドロップダウン **[!UICONTROL Products]** ストを選択します。
1. **[!UICONTROL Attribute Code]** の下にリストされている **[!UICONTROL status]** を検索します。 この属性コードは、使用可能な属性のリスト（**[!UICONTROL Enable Product]**）に表示されます。
1. 「**[!UICONTROL Export]**」をクリックします。

<u> 期待される結果：</u>

書き出したばかりの CSV ファイルには、「[!UICONTROL status]」というラベルの付いた列が表示されます。

<u> 実際の結果：</u>

書き出された csv ファイルには、[!UICONTROL status] というラベルの付いた列は表示されません。

## 原因：

CSV ファイル内の製品のステータス属性の名前が変更されました。 現在は [!UICONTROL product_online] 列です。

## 解決策

1. 「**[!UICONTROL System]**」を選択し、「**[!UICONTROL Import]**」の下 **[!UICONTROL Data Transfer]** ある「」を選択します。
1. 「**[!UICONTROL Download Sample File]**」をクリックします。
1. [!UICONTROL product_online] の列は CSV ファイルで表示できます。

## 関連資料

* ユーザーガイドの [CSV ファイルの操作 ](https://docs.magento.com/user-guide/system/data-csv.html)。
* アドビのユーザーガイドの [ 製品書き出し属性リファレンス ](https://docs.magento.com/user-guide/system/data-attributes-product.html)。
