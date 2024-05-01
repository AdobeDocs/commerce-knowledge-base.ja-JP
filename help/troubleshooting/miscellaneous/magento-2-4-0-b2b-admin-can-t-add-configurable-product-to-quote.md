---
title: Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない
description: この記事では、B2B Quote を管理する際に、**SKU**で設定可能な商品を Quote に追加できない、Commerce Admin の既知の問題について説明します。 「**Quote に追加**」ボタンをクリックすると、**Quote**編集ページの読み込みが停止し、製品を設定して変更を保存することができません。 この問題は、管理者が、**SKU**で注文に製品を追加する場合や、**高度なチェックアウト**（**管理者** &gt; **顧客** &gt; **すべての顧客** &gt; **顧客編集** &gt; **買い物かごを管理**）で**SKU**で製品を追加する場合にも発生します。 この問題は、Adobe Commerce 2.4.1 のパッチで解決されます。
exl-id: 73f7231b-b496-4250-b9e2-29427c772d56
feature: Admin Workspace, B2B, Catalog Management, Configuration, Products, Quotes
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない

この記事では、B2B Quote を管理する際、次の方法では設定可能な商品を追加できない、Commerce Admin の既知の問題について説明します **SKU** を引用符に変更します。 をクリックしたとき **見積もりに追加** ボタン、 **見積もり** 編集ページの読み込みが停止しており、製品を設定して変更を保存することができません。 この問題は、によって製品を追加した場合にも管理者で発生します。 **SKU** オーダーに追加する製品 **SKU** 。対象： **高度なチェックアウト** （**Admin** > **顧客** > **すべての顧客** > **顧客の編集** > **買い物かごの管理**）に設定します。 この問題は、Adobe Commerce 2.4.1 のパッチで解決されます。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

## 問題

<u>前提条件</u>

* Adobe Commerce 2.4.0 がインストールされています。
* B2B がインストールされています。
* B2B 機能をに設定 **会社を有効にする=**  *はい* , **共有カタログを有効にする=**  *不可* 、および **B2B の見積もりを有効にする=**  *はい*.
* 顧客アカウントを作成します。
* 以前に作成した顧客を会社管理者として使用して、会社アカウントを作成します。
* シンプルな製品の作成（例：名前および **SKU** = TEST SIMPLE 1）に割り当てられていません **デフォルト （一般）**.
* 上記で作成した簡単な製品を使用して、会社の管理者に見積もりを依頼します（例：TEST SIMPLE 1）。

<u>再現手順</u>

1. Commerce管理パネルに移動します。
1. に移動 **売上/見積**.
1. を開きます **見積もり**.
1. 「」をクリックします **SKU で製品を追加** ボタン。
1. を入力 **SKU** 別の製品（例：TEST SIMPLE 2）を **SKU を入力** 入力フィールド。
1. に有効な数量を入力 **数量** 入力フィールド。
1. 「」をクリックします **見積もりに追加** ボタン。

<u>期待される結果</u>

* この **Quote に追加されていない製品** グリッド（名前と **SKU** 作成した製品のうち、が期待どおりに表示されます。
* 製品を設定すると、管理者はに追加できるようになります **見積もり** をクリックする **製品を見積もりに追加** ボタン（期待どおり）。

<u>実際の結果</u>

* この **Quote に追加されていない製品** グリッド（名前と **SKU** 作成された製品のは表示されません。
* この **見積もり** ページの読み込みが停止しています。

## 推奨事項

現在、B2B 見積書の編集に関しては、この問題に対する回避策はありませんが、注文と買い物かごの管理については、から製品を選択できます **製品リスト** で追加するのではなく、 **SKU**. この問題を解決するパッチは、2020 年 Q4 のリリースが予定されているAdobe Commerce 2.4.1 で使用できます。

## 関連資料

* [Adobe Commerce 2.4.0 の既知の問題：顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー](/help/troubleshooting/storefront/magento-2-4-0-known-issue-orders-display-error.md)
