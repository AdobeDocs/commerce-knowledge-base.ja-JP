---
title: Adobe Commerce 2.3.x のExtension Managerに拡張機能が表示されない
description: この記事では、Commerce Marketplace経由で拡張機能を購入した後、Adobe Commerce 2.3.x の管理Extension Managerに拡張機能が見つからない場合の回避策を説明します。
exl-id: bed8506d-39b9-449a-891b-466d214a0fe8
feature: Extensions
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Adobe Commerce 2.3.x のExtension Managerに拡張機能が表示されない

この記事では、Commerce Marketplace経由で拡張機能を購入した後、Adobe Commerce 2.3.x の管理Extension Managerに拡張機能が見つからない場合の回避策を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerceのバージョン（すべてのデプロイメント方法） 2.3.x

## 問題

Commerce Marketplace経由で拡張機能を購入した場合、コア Adobe Commerce Extension Managerを使用してインストールすることはできません。 アクセスキーを追加して Marketplace に同期すると、Extension Managerに拡張機能が表示されません。

この問題の **回避策** は、開発者向けドキュメントの [ 一般的な CLI のインストール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions) に示されているように、コマンドライン Adobe Commerceのインストールを使用することです。

<u> 再現手順 </u>:

1. Commerce Marketplaceから拡張機能を購入します。
1. 拡張機能のアクセスキーを追加し、Marketplace に同期します。
1. 管理者の「Extension Manager」セクションに移動します。

<u> 期待される結果 </u>:

この拡張機能は、Commerce管理者の「Extension Manager」セクションに表示されます。

<u> 実際の結果 </u>:

**以下の画像のように、Commerce管理者の「Extension Manager」セクションに拡張子が表示されません。**


![KB-607_Image_1.png](assets/KB-607_Image_1.png)

## 回避策

開発者向けドキュメントの [ 一般的な CLI のインストール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions) に示されているコマンドライン Adobe Commerceのインストールを使用します。
