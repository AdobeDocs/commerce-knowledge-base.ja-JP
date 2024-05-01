---
title: クイックチェックアウトの問題のトラブルシューティング
description: この記事では、Adobe Commerceのクイックチェックアウト拡張機能の使用中に発生する可能性のある問題について説明し、拡張機能を正常に使用できるようにこれらの問題を修正するソリューションを提供します。
exl-id: 8ab46318-d62a-4b7e-bbe5-4c52cfeb9e36
feature: Checkout, Orders
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# クイックチェックアウトの問題のトラブルシューティング

この記事では、Adobe Commerceのクイックチェックアウト拡張機能の使用中に発生する可能性のある問題について説明し、拡張機能を正常に使用できるようにこれらの問題を修正するソリューションを提供します。

## 影響を受ける製品とバージョン

* この [クイックチェックアウト](https://experienceleague.adobe.com/docs/commerce-merchant-services/quick-checkout/overview.html) は、Magento Open SourceとAdobe Commerceの両方と互換性があります。 参照： [ライフサイクルポリシー](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html) サポートされているバージョンについて詳しくは、こちらを参照してください。

## 間違った Composer キーとへの最小安定性 `RC`

<u>原因：</u>:

次のエラーメッセージが表示された場合は、コンポーザーのキーが正しくない可能性があります。

```terminal
Could not find a matching version of package magento/quick-checkout. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (RC).
```

<u>解決策</u>:

コンポーザキーがにリンクされていることを確認します _MAGENTOID_ クイックチェックアウト登録時に使用されます。

設定されているコンポーザキーを確認するには：

1. の場所を検索 `auth.json` ファイル：

   ```bash
   composer config --global home
   ```

1. を表示する `auth.json` ファイル：

   ```bash
   cat /path/to/auth.json
   ```

1. 参照： [MagentoID に関連付けられているキー](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html).

1. 最小安定性を次のように設定 `RC` が含まれる `composer.json` ファイル。

   ```json
   "minimum-stability": "RC"
   ```

## PHP に必要なメモリが不足しています

<u>原因：</u>:

PHP 用のメモリが不足していることを示す次のエラーメッセージが表示された場合：

```terminal
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

<u>解決策</u>:

[メモリの上限を増やす](https://devdocs.magento.com/cloud/project/magento-app-php-ini.html#increase-php-memory-limit) 使用している環境での PHP の場合： `php.ini`.

または、次のコマンドを使用してメモリ制限を指定することもできます。 `php -d memory_limit=-1 [path to composer]/composer require magento/quick-checkout`.

例：

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/quick-checkout
```

## 新しい配送先住所を使用した番地行の追加

クイックチェックアウト拡張機能には既知の問題があります。

実行する場合 [bolt アカウントでログイン](https://help.bolt.com/shoppers/guides/checkout/log-in/)新しい配送先住所を追加できます（番地 1 件につき 4 行の制限）。

新しい配送先住所に 4 行を超える行が含まれている場合、それらは保存されません。

通常、Adobe Commerceは、最大 20 行の番地をサポートするように設定できます。

## 次の場合の予期しない動作 `Display Billing Address On` はに設定されています。 `payment page`

クイックチェックアウト拡張機能には既知の問題があります。

を設定した場合 `Display Billing Address On` のパラメーター `payment page` および [bolt アカウントでログイン](https://help.bolt.com/shoppers/guides/checkout/log-in/) を確認する場合 `My billing and shipping address are the same` チェックボックスをオンにすると、ラジオボタンが表示されます `use existing card`. 請求先住所は新しいクレジットカードにのみ適用されるため、Bolt ユーザーが新しいクレジットカードのオプションを追加することを決定するまで、住所は表示されません。

を参照してください。 [チェックアウト](https://docs.magento.com/user-guide/configuration/sales/checkout.html) に関する詳細情報のトピック `Display Billing Address On` パラメーター。
