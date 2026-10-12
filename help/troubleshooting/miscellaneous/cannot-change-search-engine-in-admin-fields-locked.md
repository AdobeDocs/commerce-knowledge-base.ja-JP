---
title: 「app/etc/env.php」の検索エンジンを変更できません
description: この記事では、Commerce Adminで検索エンジンを変更しようとしたが、フィールドがロックされる問題の解決策を示します。
exl-id: 61006ce7-34f9-4e4d-a197-f3d627dd277f
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%
---
# `app/etc/env.php`の検索エンジンを変更できません

この記事では、`app/etc/env.php` ファイルから検索エンジン設定を削除しようとしたが、再デプロイメント後、設定は以前の設定に戻るか、デフォルトで[!DNL OpenSearch]に変更される問題の解決策を示します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、[ サポートされているすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## イシュー

Commerce Adminで検索エンジンを変更しようとしましたが、フィールドがロックされています。

## 原因

検索エンジンの設定が`app/etc/env.php` ファイルでロックされているか、検索エンジンが`.magento.env.yaml` ファイルで明示的に定義されています。

## Solution

1. デプロイ段階の`.magento.env.yaml` ファイルを確認し、`SEARCH_CONFIGURATION`変数が設定されているかどうかを確認します。 例：

   ```yaml
   SEARCH_CONFIGURATION:
     engine: elasticsearch7
     ...
   <VARIABLE X>
   ```

1. `SEARCH_CONFIGURATION`変数は存在しますか？ 存在しない場合、検索エンジン設定はデフォルトで[!DNL OpenSearch]にロックされます。 設定を変更するには、検索エンジンに適切な値を持つ`.magento.env.yaml` ファイルに変数を追加する必要があります。 `SEARCH_CONFIGURATION`変数が存在し、エンジンを変更する場合は、`.magento.env.yaml`のエンジンの既存の値を置き換えます。 使用可能な値：[!DNL opensearch]、[!DNL livesearch]、[!DNL elasticsuite]、[!DNL amasty_elastic]、および[!DNL amasty_elastic_opensearch]。
1. インスタンスを再デプロイします。
1. 管理者の検索エンジンフィールドはロックされたままですが、指定した値で更新されます。

## 関連トピックス

* Commerce on Cloud Infrastructure ガイドのCommerce Admin](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26879)の[ ロック（グレー表示）フィールド。
