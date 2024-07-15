---
title: 2.4.4 から 2.4.4-p1 へのアップグレード後にダウングレードされたパッケージ
description: この記事では、バージョン 2.4.4 のマーチャントが「composer update」コマンドを実行し、次に示すパッケージ（モジュール）が以前のバージョンにダウングレードされる問題のホットフィックスを提供します。以前のバージョンはバージョン 2.4.4 と互換性がなく、バージョン 2.4.5 以降でのみ使用することが想定されています。
exl-id: 4ebdbcd7-6905-4647-b071-1e4413455f38
feature: Upgrade
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 2.4.4 から 2.4.4-p1 へのアップグレード後にダウングレードされたパッケージ

この記事では、バージョン 2.4.4 のマーチャントが `composer update` コマンドを実行した後、次に示すパッケージ（モジュール）が以前のバージョンにダウングレードされる問題のホットフィックスを提供します。以前のバージョンは、バージョン 2.4.4 と互換性がなく、バージョン 2.4.5 以降でのみ使用することが想定されています。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.4 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.4
* Magento Open Source 2.4.4

## 問題

この問題がどのように発生するか、どのように再現できるかは、2 つのシナリオがあります。

### シナリオ 1

<u> 再現手順 </u>:

2.4.4 から 2.4.4-p1 にアップグレードする場合、同様の出力でダウングレードされる多数のパッケージ（モジュール）があります。

```text
Downgrading magento/module-adobe-ims (2.1.4 => 2.1.3)
Downgrading magento/module-adobe-ims-api (2.1.2 => 2.1.1)
Downgrading magento/module-adobe-stock-admin-ui (1.3.2 => 1.3.1)
Downgrading magento/module-adobe-stock-client-api (2.1.2 => 2.1.1)
Downgrading magento/module-adobe-stock-image (1.3.3 => 1.3.2)
Downgrading magento/module-adobe-stock-image-admin-ui (1.3.3 => 1.3.2)
Downgrading magento/module-banner-page-builder (2.2.3 => 2.2.2)
Downgrading magento/module-inventory (1.2.3 => 1.2.2)
Downgrading magento/module-inventory-admin-ui (1.2.3 => 1.2.2-p1)
Downgrading magento/module-inventory-advanced-checkout (1.2.2 => 1.2.1)
Downgrading magento/module-inventory-api (1.2.3 => 1.2.2-p1)
Downgrading magento/module-inventory-bundle-product (1.2.2 => 1.2.1)
Downgrading magento/module-inventory-catalog-api (1.3.3 => 1.3.2)
Downgrading magento/module-inventory-configurable-product-admin-ui (1.2.3 => 1.2.2-p1)
Downgrading magento/module-inventory-configurable-product-frontend-ui (1.0.3 => 1.0.2)
Downgrading magento/module-inventory-import-export (1.2.3 => 1.2.2)
Downgrading magento/module-inventory-in-store-pickup-admin-ui (1.1.2 => 1.1.1)
Downgrading magento/module-inventory-in-store-pickup-frontend (1.1.3 => 1.1.2)
Downgrading magento/module-inventory-in-store-pickup-graph-ql (1.1.2 => 1.1.1)
Downgrading magento/module-inventory-in-store-pickup-sales-admin-ui (1.1.3 => 1.1.2-p1)
Downgrading magento/module-inventory-in-store-pickup-shipping (1.1.2 => 1.1.1)
Downgrading magento/module-inventory-low-quantity-notification (1.2.2 => 1.2.1)
Downgrading magento/module-inventory-low-quantity-notification-api (1.2.2 => 1.2.1-p1)
Downgrading magento/module-inventory-requisition-list (1.2.3 => 1.2.2)
Downgrading magento/module-inventory-sales-admin-ui (1.2.3 => 1.2.2)
Downgrading magento/module-inventory-sales-api (1.2.2 => 1.2.1)
Downgrading magento/module-inventory-shipping-admin-ui (1.2.3 => 1.2.2-p1)
Downgrading magento/module-inventory-source-selection-api (1.4.2 => 1.4.1-p1)
Downgrading magento/module-inventory-wishlist (1.0.2 => 1.0.1)
Downgrading magento/module-page-builder (2.2.3 => 2.2.2)
Downgrading magento/module-re-captcha-checkout-sales-rule (1.1.1 => 1.1.0)
Downgrading magento/module-re-captcha-customer (1.1.3 => 1.1.2)
Downgrading magento/module-re-captcha-frontend-ui (1.1.3 => 1.1.2)
Downgrading magento/module-staging-page-builder (2.2.3 => 2.2.2)
Downgrading magento/module-two-factor-auth (1.1.4 => 1.1.3)
Removing magento/module-admin-adobe-ims (100.4.0)
```

<u> 期待される結果 </u>:

バージョン 2.4.4 から 2.4.4-p1 にアップグレードすると、バージョン 2.4.4-p1 の正しいパッケージ（モジュール）が得られます。

<u> 実際の結果 </u>:

バージョン 2.4.4 から 2.4.4-p1 へのアップグレード中に、これらのパッケージのバージョン（モジュールのバージョン）はダウングレードされますが、これらのメッセージは無視でき、機能には影響しません。

### シナリオ 2

<u> 再現手順 </u>:

2.4.4 マーチャントが `composer update` コマンドを実行すると、上記 **シナリオ 1** で示したのと同じパッケージ（モジュール）が、バージョン 2.4.5 とのみ互換性があり、バージョン 2.4.4 では使用されない新しいバージョンにアップグレードされます。

<u> 期待される結果 </u>:

バージョン 2.4.4 から 2.4.4-p1 にアップグレードすると、バージョン 2.4.4-p1 の正しいパッケージ（モジュール）が得られます。

<u> 実際の結果 </u>:

パッケージ（モジュール）は、バージョン 2.4.4 から 2.4.4-p1 にアップグレードした後、ダウングレードされます。

## 回避策 1：パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後までスクロールしてファイル名をクリックするか、次のリンクをクリックします。[ ダウンロード ACPLTSRV-2017-fix.sh.zip](assets/ACPLTSRV-2017-fix.sh.zip)

## 互換性のあるAdobe CommerceおよびMagento Open Sourceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.4.4 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.4
* Magento Open Source 2.4.4

>[!NOTE]
>
>このパッチは、他のAdobe CommerceおよびMagento Open Sourceのバージョンやエディションとは互換性がありません。

## パッチの適用方法

添付の bash スクリプト [ACPLTSRV-2017-fix.sh.zip](assets/ACPLTSRV-2017-fix.sh.zip) を、この問題の回避策として使用します。

**スクリプトの使用方法の正確な説明：**

### クラウドインフラストラクチャー上のAdobe Commerceの場合：

1. クラウドコードベースのローカルチェックアウト `ACPLTSRV-2017-fix.sh` に bash スクリプトファイルをダウンロードします。
1. bash スクリプト ファイル `ACPLTSRV-2017-fix.sh` を実行して、composer ファイルをローカルで変更します。
1. 変更した Composer ファイルを追加して Git リポジトリにコミットします。

### Adobe CommerceまたはMagento Open Source オンプレミス：

1. bash スクリプト `ACPLTSRV-2017-fix.sh` を、Adobe Commerce/Magento Open Source 2.4.4 のインストール先の `root` フォルダー（`composer.json` と同じフォルダー）に配置します。
1. `apply` 引数を指定して bash スクリプトを実行し、影響を受けるパッケージ（モジュール）を 2.4.4 バージョンにロックします。

   ```bash
   sh ACPLTSRV-2017-fix.sh apply
   ```

1. 更新された composer を実行して、ロックされたパッケージ（モジュール）をインストールします。
1. 2.4.5 または 2.4.4-p1 にアップグレードする準備ができたら、`rollback` の引数を指定してスクリプトを実行します。

   ```bash
   sh ACPLTSRV-2017-fix.sh rollback
   ```

   この手順をスキップすると、パッケージ（モジュール）要件の競合が原因でアップグレードエラーが発生します。
1. 上記の手順が完了したら、アップグレードを開始できます。

## 回避策 2

この問題の 2 つ目の回避策は、引数を指定せずに `composer update` コマンドを実行しないことです。
