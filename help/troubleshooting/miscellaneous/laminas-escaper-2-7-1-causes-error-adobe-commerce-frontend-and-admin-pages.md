---
title: laminas/laminas-escaper 2.7.1 でAdobe Commerceのフロントエンドおよび管理ページのエラーが発生する
description: この記事では、laminas/laminas-escaper:2.7.1 のリリースによってAdobe Commerceの製品管理、カテゴリおよび製品ページの機能が損なわれている問題の解決策について説明します。 この問題は、Adobe Commerce 2.4.3 で修正されます。
exl-id: 89de6827-7b90-4f08-92fb-56ed31ae2672
feature: Admin Workspace, Categories
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# laminas/laminas-escaper 2.7.1 でAdobe Commerceのフロントエンドおよび管理ページのエラーが発生する


## 影響を受ける製品とバージョン

* クラウドアーキテクチャ 2.3.5 以降でのAdobe Commerce
* Adobe Commerce 2.3.5 以降

## 問題

ラミナス/ラミナス – エスケープ：2.7.1 に更新すると、エラーメッセージがページに表示されます。

<u> 再現手順 </u>:

Laminas/laminas-escaper を 2.7.1 に更新します。

<u> 期待される結果 </u>:

エラーはありません。

<u> 実際の結果 </u>:

laminas/laminas-escaper:2.7.1 に更新すると、製品編集（または製品管理）ページにエラーメッセージが表示されます。*TypeError: rawurlencode （）は、/var/www/magento/vendor/laminas/laminas-escaper/src/Escaper.php:246 で指定された int のパラメータ 1 が文字列であることを想定し* す。
このエラーは、フロントエンドページと管理ページで発生し、ページのコンテンツが歪みます。

## 原因：

laminas/laminas-escaper 2.7.1 では、Escaper クラスの厳密な型検証を使用し始めました。

## 解決策

各プロジェクトのルートディレクトリで `composer require laminas/laminas-escaper:2.7.0` を実行します。

## 関連資料

laminas ドキュメント：[laminas-escaper](https://docs.laminas.dev/laminas-escaper/)
