---
title: Adobe Commerceでキャッシュのウォーミングアップとサイトを利用できない
description: この記事では、ページキャッシュがウォームアップ中で、デプロイメントまたはサイトが停止している場合の解決策を提供します。
exl-id: c91d5c1f-95e6-4240-be98-2acea49ae728
feature: Cache, Variables
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
  - id: 2191e157-828a-5358-ad69-ebcaa8402915
    internal-label: Variables
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%
---
# Adobe Commerceでキャッシュのウォーミングアップとサイトを利用できない

この記事では、ページキャッシュがウォームアップ中で、デプロイメントまたはサイトが停止している場合の解決策を提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、すべての[&#x200B; サポートされているバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。

## イシュー

デプロイ後のフェーズの終了時に、キャッシュウォームアップスクリプトは、特定のインスタンス（4 cpuなど）が対処できないような高いレートでリクエストを送信します。 彼らのnginxは労働者の数を使い果たします。

<u>複製する手順</u>:

キャッシュ ウォームアップ操作を開始します。

<u>期待される結果</u>:

ページまたはサイト全体が読み込まれます。

<u>実際の結果</u>:

サイトが利用できないか、応答時間が長すぎます。

## Solution

キャッシュウォームアップ中の同時接続数を制限します。 これには、キャッシュウォームアップスクリプトが同時に送信できるウォームアップリクエストの数を指定するために、`WARM_UP_CONCURRENCY` デプロイ後の変数を追加する必要があります。 このオプションを設定すると、Adobe Commerce クラウドインフラストラクチャの負荷を管理するのに役立ちます。 手順については、開発者ドキュメントの[&#x200B; デプロイ後の変数/WARM\_UP\_CONCURRENCY](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-post-deploy#warm_up_concurrency)を参照してください。

## 関連トピックス

ユーザーガイドの[&#x200B; フルページキャッシュ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/cache-management#full-page-caching)
