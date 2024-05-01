---
title: 「app/etc/env.php」の検索エンジンを変更できません
description: この記事では、Commerce管理者で検索エンジンを変更しようとすると、フィールドがロックされる問題の解決策を提供します。
exl-id: 61006ce7-34f9-4e4d-a197-f3d627dd277f
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# の検索エンジンを変更できません `app/etc/env.php`

この記事では、から検索エンジン設定を削除しようとする問題の解決策を提供します `app/etc/env.php` ファイルを再デプロイした後に、設定が以前の設定に戻るか、に変更されます。 [!DNL OpenSearch] デフォルトでは。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce [すべてのサポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

Commerce Admin で検索エンジンを変更しようとすると、フィールドがロックされる。

## 原因：

検索エンジンの設定は、 `app/etc/env.php` ファイルまたは検索エンジンが `.magento.env.yaml` ファイル。

## 解決策

1. を確認します `.magento.env.yaml` デプロイステージの下のファイルで、 `SEARCH_CONFIGURATION` 変数が設定されています。 例：

   ```yaml
   SEARCH_CONFIGURATION:
     engine: elasticsearch7
     ...
   <VARIABLE X>
   ```

1. が  `SEARCH_CONFIGURATION` 変数が存在する場合 存在しない場合、検索エンジン設定はロックされます [!DNL OpenSearch] デフォルトでは。 設定を変更するには、変数をに追加する必要があります。 `.magento.env.yaml` 検索エンジンに適した値を持つファイル。 次の場合 `SEARCH_CONFIGURATION` 変数が存在しており、エンジンを変更する場合は、にあるエンジンの既存の値を `.magento.env.yaml`. 可能な値/既知の値： [!DNL opensearch], [!DNL livesearch], [!DNL elasticsuite], [!DNL amasty_elastic]、および [!DNL amasty_elastic_opensearch].
1. インスタンスを再デプロイします。
1. 管理者の検索エンジンフィールドはロックされたままになりますが、指定した値で更新される必要があります。

## 関連資料

* [Commerce Admin でロックされたフィールド](/help/troubleshooting/miscellaneous/locked-fields-in-magento-admin.md) （クラウドインフラストラクチャー上のCommerceに関するガイド）を参照してください。
