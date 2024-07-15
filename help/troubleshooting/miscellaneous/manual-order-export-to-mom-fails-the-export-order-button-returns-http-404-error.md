---
title: MOM への手動オーダーのエクスポートが失敗する。 「書き出し順序」ボタンが HTTP 404 エラーを返す
description: この記事では、Commerce Admin の注文ビューで「注文を書き出す**ボタンをクリックして注文をMagento Order Management（MOM）に書き出そうとすると**「*404 Page Not Found*」エラーが返される問題を修正する方法を説明します。
exl-id: 75741473-7c9a-4418-a56f-de75ac246d27
feature: Data Import/Export
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# MOM への手動オーダーのエクスポートが失敗する。 「書き出し順序」ボタンが HTTP 404 エラーを返す

この記事では、Commerce Admin の注文ビューで「注文を書き出す **ボタンをクリックして注文をMagento Order Management（MOM）に書き出そうとすると** 「*404 Page Not Found*」エラーが返される問題を修正する方法を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.2.x, 2.3.x#キョウジ 2.2.x#
* MOM コネクタ 2.3.0、2.4.0、3.2.0、3.3.0

## 問題

<u> 再現手順：</u>:

1. Commerce Admin で、**Sales > Orders** をクリックします。
1. 「**新しい注文を作成** ボタンをクリックします。
1. ユーザーを選択し、項目を追加し、支払い方法と発送方法を選択して、「**注文を送信**」ボタンをクリックします。
1. 「**書き出し順序**」ボタンをクリックし、「**OK**」をクリックします。

<u> 期待される結果 </u>:

注文は MOM に送信されます。

<u> 実際の結果 </u>:

「*404 エラー：ページが見つかりません*」ページが表示されます。

## 解決策

* Adobe Commerce 2.3.x の MOM コネクタを 3.4.0 に、またはAdobe Commerce 2.2.x の MOM コネクタ 2.5 にアップグレードします。
* MOM コネクタをアップグレードできない場合は、CLI コマンドを使用してオーダーをMagento Order Managementにエクスポートできます。

```bash
$bin/magento oms:orders:sync
```

## 関連資料

[Magento Order Management技術ドキュメント ](https://omsdocs.magento.com/en/)
