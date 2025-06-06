---
title: Braintree支払いが有効な場合、管理者が注文の作成/並べ替えを行うことはできません
description: この記事では、Adobe Commerce 2.4.5 の問題を修正するパッチを説明します。この問題では、管理者ユーザーは、Braintree支払い方法が有効な場合、お客様の注文の作成や並べ替えができない場合があります。
exl-id: 8840aecb-21d9-4965-8c09-395e2d263aaa
feature: Admin Workspace, Native Luma Frontend Development, Orders, Payments
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Braintree支払いが有効な場合、管理者が注文の作成/並べ替えを行うことはできません

この記事では、Adobe Commerce 2.4.5 の問題を修正するパッチを説明します。この問題では、管理者ユーザーは、Braintree支払い方法が有効な場合、お客様の注文の作成や並べ替えができない場合があります。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.5 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.5
* Magento Open Source 2.4.5

## 問題

<u> 再現手順 </u>:

1. コアBraintreeの統合が使用されます（**Stores**/**Configurations**/**Sales**/**Payment Method**/**8&rbrace;Braintree）。**
1. Luma ストアフロントを使用して、注文します。
1. 管理 UI / **営業** に移動します。
1. 顧客の新しい注文を作成するか、以前に注文した注文に移動して、「**並べ替え**」をクリックします。

<u> 期待される結果 </u>:

管理者ユーザーは、Braintree支払い方法が有効になっている場合、顧客の注文と並べ替えを正常に作成できます。

<u> 実際の結果 </u>:

Braintree支払い方法が有効な場合、管理者ユーザーは顧客の注文の作成や並べ替えをおこなうことができず、次のエラーが返されます。

```bash
report.CRITICAL: Error: Call to a member function getMethodInstance() on null in /app/vendor/paypal/module-braintree-core/Block/Form.php:174
```

## 原因：

クラス依存関係が正しくありません（`vendor/paypal/module-braintree-core/Block/Form.php`）

## 解決策

この記事で提供されているパッチを適用します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、次のリンクをクリックします。

[BUNDLE-3137-composer.patch.zip](assets/BUNDLE-3137-composer.patch.zip)

>[!NOTE]
>
>さらに、クラウドインフラストラクチャマーチャント上のAdobe Commerceの場合：Adobeでは、Commerce バージョン 1.0.18 のクラウドパッチの修正が含まれています。最新のパッケージを適用する手順については、開発者向けドキュメントの [Commerce リリースノートのクラウドパッチ ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/release-notes/cloud-patches) を参照してください。

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.4.5 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.5
* Magento Open Source 2.4.5

>[!NOTE]
>
>このパッチは、他のAdobe CommerceおよびMagento Open Sourceのバージョンやエディションとは互換性がありません。

## パッチの適用方法

手順については、サポートナレッジベースの [Adobe提供の Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。
