---
title: Adobe Commerce 2.4.4 にないモジュール
description: ここでは、以前のAdobe Commerce バージョンに含まれているモジュールが 2.4.4 に存在しない場合の問題の解決策について説明します。
exl-id: c0335b66-803b-44d7-b966-7d60a5f21d8d
feature: Extensions
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Adobe Commerce 2.4.4 にないモジュール

この記事では、以前のAdobe Commerce バージョンに含まれているモジュールが 2.4.4 に存在しない場合の解決策を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）すべて  [サポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 問題

サードパーティ製モジュールをインストールできない、またはAdobe Commerce 2.4.4 にアップグレードしたときに、コアバンドルされた拡張機能の一部が存在しないことが判明した。この問題は、Adobe Commerce 2.4.4 から削除されたバンドル拡張機能のいずれかが必要なサードパーティモジュールをインストールした場合、またはプロジェクトが削除されたモジュールの機能の一部を使用する場合にのみ発生します。

* シナリオ 1：プロジェクトでは、コアバンドルモジュールの機能の 1 つを使用しています。 使用されているバンドルモジュールは、Adobe Commerce 2.4.4 には含まれていません。Adobe Commerce 2.4.4 へのアップグレードに成功すると、モジュールと提供された機能が見つからなくなります。

* シナリオ 2：現在のプロジェクトにインストールされているモジュールで、削除されたバンドルモジュールのいずれかに依存しているもの。

ベンダーバンドルの拡張機能はAdobe Commerce 2.4.4 コードベースから削除されているので、これは想定されている動作です。

## 解決策

公式の拡張機能を個別にインストールまたは購入します。 これらはで利用できます [Commerce Marketplace](https://marketplace.magento.com/extensions.html).

## 関連資料

[ベンダーバンドルの拡張機能](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/adobe-commerce/2-4-4.html?#vendor-bundled-extensions) Adobe Commerceのドキュメント / リリース情報/ Adobe Commerce 2.4.4 リリースノート。
