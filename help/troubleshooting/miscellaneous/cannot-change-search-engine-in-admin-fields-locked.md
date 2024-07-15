---
title: 「app/etc/env.php」の検索エンジンを変更できません
description: この記事では、Commerce管理者で検索エンジンを変更しようとすると、フィールドがロックされる問題の解決策を提供します。
exl-id: 61006ce7-34f9-4e4d-a197-f3d627dd277f
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# `app/etc/env.php` の検索エンジンを変更できません

この記事では、`app/etc/env.php` ファイルから検索エンジンの構成を削除しようとして、展開し直した後に構成が以前の設定に戻ったり、既定で [!DNL OpenSearch] に変更されたりする問題の解決策を示します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

Commerce Admin で検索エンジンを変更しようとすると、フィールドがロックされる。

## 原因：

検索エンジンの設定が `app/etc/env.php` ファイルでロックされているか、検索エンジンが `.magento.env.yaml` ファイルで明示的に定義されています。

## 解決策

1. デプロイステージの下の `.magento.env.yaml` ファイルを確認し、`SEARCH_CONFIGURATION` 変数が設定されているかどうかを確認します。 例：

   ```yaml
   SEARCH_CONFIGURATION:
     engine: elasticsearch7
     ...
   <VARIABLE X>
   ```

1. `SEARCH_CONFIGURATION` 変数は存在しますか？ 存在しない場合、検索エンジン設定は、デフォルトで [!DNL OpenSearch] にロックされます。 設定を変更するには、変数を `.magento.env.yaml` ファイルに追加し、検索エンジンに適した値を指定する必要があります。 `SEARCH_CONFIGURATION` 変数が存在し、エンジンを変更する場合は、`.magento.env.yaml` のエンジンの既存の値を置き換えます。 可能な値/既知の値：[!DNL opensearch]、[!DNL livesearch]、[!DNL elasticsuite]、[!DNL amasty_elastic]、[!DNL amasty_elastic_opensearch]。
1. インスタンスを再デプロイします。
1. 管理者の検索エンジンフィールドはロックされたままになりますが、指定した値で更新される必要があります。

## 関連資料

* [ クラウドインフラストラクチャー上のCommerceのCommerce管理者 ](/help/troubleshooting/miscellaneous/locked-fields-in-magento-admin.md) でロックされたフィールド」ガイド。
