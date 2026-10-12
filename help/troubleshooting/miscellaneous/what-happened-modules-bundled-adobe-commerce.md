---
title: Adobe Commerce 2.4.4にモジュールが見つからない
description: この記事では、以前のAdobe Commerce バージョンに含まれているモジュールが2.4.4に存在しない場合の問題に対する解決策を提供します。
exl-id: c0335b66-803b-44d7-b966-7d60a5f21d8d
feature: Extensions
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
subfeature_v2:
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
    internal-label: Extensions
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%
---
# Adobe Commerce 2.4.4にモジュールが見つからない

この記事では、以前のAdobe Commerce バージョンに含まれているモジュールが2.4.4に存在しない場合の解決策を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce （すべてのデプロイメント方法）すべての[&#x200B; サポートされているバージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## イシュー

Adobe Commerce 2.4.4へのアップグレード時に、サードパーティ製モジュールをインストールできないか、一部のコアバンドル拡張機能が存在しないことが判明した。 これは、Adobe Commerce 2.4.4から削除されたバンドル拡張機能のいずれかを必要とするサードパーティモジュールをインストールするか、削除されたモジュールの1つの機能をプロジェクトで使用する場合にのみ発生します。

* シナリオ 1: プロジェクトで、コアバンドルモジュールの1つの機能が使用されている。 使用されるバンドルモジュールは、Adobe Commerce 2.4.4には含まれていません。 Adobe Commerce 2.4.4へのアップグレードが正常に完了した後、モジュールとその提供される機能が欠落していることに気付きます。

* シナリオ 2：現在のプロジェクトに、削除されたバンドルモジュールのいずれかに依存するモジュールがインストールされている。

Vendor-Bundled ExtensionsがAdobe Commerce 2.4.4 コードベースから削除されたため、この動作が期待されます。

## Solution

公式の拡張機能は個別にインストールまたは購入してください。 これらは、[Commerce Marketplace](https://marketplace.magento.com/extensions.html)で利用できます。

## 関連トピックス

Adobe Commerce ドキュメント/リリース情報/Adobe Commerce 2.4.4 リリースノートの[Vendor-Bundled Extensions](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/adobe-commerce/2-4-4.html?#vendor-bundled-extensions)を参照してください。
