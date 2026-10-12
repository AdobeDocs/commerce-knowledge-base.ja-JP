---
title: 書き出された商品のCSV ファイルが見つからないAdobe Commerce ステータス列
description: この記事では、書き出された製品を含むCSV ファイルでステータス列が見つからない場合の問題の解決策を示します。
exl-id: 3cbe1e6c-fc73-4331-add7-1ebcb28a4580
feature: Data Import/Export, Products
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%
---
# 書き出された商品のCSV ファイルが見つからないAdobe Commerce ステータス列

この記事では、書き出された製品を含むCSV ファイルにステータス列（製品が有効か無効かを示す）が見つからない場合の問題の解決策を示します。 製品のステータスは、[!UICONTROL product_online]列で示されます。

## 影響を受ける製品とバージョン

Adobe Commerce （すべてのデプロイメント方法）すべての[&#x200B; サポートされているバージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## イシュー

書き出された製品を含むCSV ファイルの[!UICONTROL status]列が見つかりません。 例えば、すべてのSKUのCSVをステータスで書き出しますが、テーブルに[!UICONTROL status]列がないようです。

<u>再生する手順：</u>

1. Adobe Commerce Adminで、**[!UICONTROL System]**&#x200B;を選択し、**[!UICONTROL Data Transfer]**&#x200B;の下の&#x200B;**[!UICONTROL Export]**&#x200B;を選択します。
1. **[!UICONTROL Export Settings]** セクションで、**[!UICONTROL Entity Type]** ドロップダウン **[!UICONTROL Products]**&#x200B;を選択します。
1. **[!UICONTROL Attribute Code]**&#x200B;の下にリストされている&#x200B;**[!UICONTROL status]**&#x200B;を検索します。 使用可能な属性（**[!UICONTROL Enable Product]**）のリストに、その属性コードが表示されます。
1. **[!UICONTROL Export]**&#x200B;をクリックします。

<u>期待される結果：</u>

先ほどエクスポートしたCSV ファイルに、[!UICONTROL status]というラベルの付いた列が表示されます。

<u>実際の結果：</u>

書き出されたcsv ファイルに「[!UICONTROL status]」というラベルの付いた列が表示されません。

## 原因

製品のstatus属性の名前がCSV ファイルで変更されました。 これで[!UICONTROL product_online]列になりました。

## Solution

1. **[!UICONTROL Data Transfer]**&#x200B;の下の&#x200B;**[!UICONTROL System]**&#x200B;を選択し、**[!UICONTROL Import]**&#x200B;を選択します。
1. **[!UICONTROL Download Sample File]**&#x200B;をクリックします。
1. CSV ファイルに[!UICONTROL product_online]列が表示されます。

## 関連トピックス

* ユーザーガイドの[CSV ファイルの操作](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-csv)。
* ユーザーガイドの[製品書き出し属性リファレンス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-attributes-product)。
