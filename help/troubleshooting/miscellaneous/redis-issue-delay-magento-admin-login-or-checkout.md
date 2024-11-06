---
title: Redis 問題により、Commerce管理者のログインまたはチェックアウトが遅れる
description: この記事では、Commerce管理者にログインしたり、チェックアウトページを開いたりすると、遅延やタイムアウト（30 秒以上）が発生する問題を修正しました。 この問題は、Redis がセッションストレージに使用されている場合に発生します。
exl-id: a91a7a51-7cc4-4910-a9de-3a212788663f
feature: Admin Workspace, Checkout, Orders, Services
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Redis 問題により、Commerce管理者のログインまたはチェックアウトが遅れる

この記事では、Commerce管理者にログインしたり、チェックアウトページを開いたりすると、遅延やタイムアウト（30 秒以上）が発生する問題を修正しました。 この問題は、Redis がセッションストレージに使用されている場合に発生します。

**原因：**   [Github の問題\#12385](https://github.com/magento/magento2/issues/12385)。

**解決策：** Redis のすべてのバージョンとAdobe Commerceの特定のバージョンに関する問題を修正するには、最新のAdobe Commerce パッチに更新してください。

## 影響を受けるバージョンとテクノロジー

* cloud infrastructure 上のAdobe Commerceのバージョン 2.1.11 ～ 2.1.13 および 2.2.1
* Adobe Commerce オンプレミスのバージョン 2.1.11 ～ 2.1.13 および 2.2.1
* Redis、すべてのバージョン

クラウドインフラストラクチャバージョン [2.2.0](#h_64593789291526919876198) でAdobe Commerceを使用している場合は、回避策が利用可能です。

## 問題

Commerce管理者にログインするか、チェックアウトページに進むには、30 秒以上かかります。

これは、ユーザーセッションが Redis に保存されている場合にのみ発生します。

## 原因：

Adobe Commerceには、セッションロックのメカニズムに問題があり、Redis をセッションストレージに使用した際に、一部のオペレーションで 30 秒のタイムアウトが追加されました。 詳しくは、[Github の問題\#12385](https://github.com/magento/magento2/issues/12385) を参照してください。

この問題は、Adobe Commerce 2.1.14 および 2.2.2 で修正されました。

## ソリューション：パッチまたはアップグレード

### 解決策 1：修正プログラムを適用する

パッチを受け取るには、パッチをリクエストする [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) します。 チケットに、Adobe Commerceのバージョンと、パッチに対応する参照番号を指定します。

* **2.1.11 以降：** MDVA-7835
* **2.2.1:** MDVA-8128

一般的な（バージョンに依存しない）参照番号は MAGETWO-84289 です。

### 解決策 2: 2.1.14/2.2.2以降へのアップグレード

以前にAdobe Commerce 2.2.2 以降へのアップグレードを検討した場合は、このアップデートの機会を利用して問題を修正することができます。

## 回避策：セッションロックを無効にします

セッションロックを無効にするには、`env.php` ファイルの Redis 設定セクションで `disable_locking` を `1` に設定します。

```php
'session' =>
  array (
    'save' => 'redis',
    'redis' =>
    array (
      'host' => 'redis.internal',
      'port' => 6379,
      'database' => '0',
      'disable_locking' => '1'
    ),
  ),
```

このソリューションは、他のAdobe Commerce機能には影響しません。

### パッチ適用後に回避策を元に戻す

修正を含むパッチを適用した後は、回避策は不要になったので、それを元に戻すことができます（`disable_locking` を `0` に設定）。

## Adobe Commerce on cloud infrastructure 2.2.0: ECE-Tools v2002.0.8 以降を使用します {#h_64593789291526919876198}

バージョン 2002.0.3 ～ 2002.0.7 の [ECE-Tools](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package) デプロイメントスクリプトパッケージ [ 適用 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package.html) この回避策は自動的に `disable_locking` を `1` に設定します。 これにより、元の問題が発生しないAdobe Commerce 2.2.0 のセッションロック機能が無効になります。

Adobe Commerceを Cloud Infrastructure 2.2.0 で実行している場合は、ECE-Tools を v2002.0.8 以降にアップグレードします。 また、クラウドインフラストラクチャー上のAdobe Commerceを 2.2.2 以降にアップグレードすることを検討することもできます。
