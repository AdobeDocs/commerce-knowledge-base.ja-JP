---
title: 'ERROR: クラウドインフラストラクチャ上のAdobe Commerceでウォームアップに失敗しました'
description: この記事では、ページキャッシュがウォーミングアップ中にエラーで失敗した場合の解決策を提供します。
exl-id: 20a88030-b1c9-4fdc-83c1-f344d44cd2e1
feature: Cache, Cloud, Paas
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%
---
# ERROR: クラウドインフラストラクチャ上のAdobe Commerceでウォームアップに失敗しました

この記事では、ページキャッシュがウォーミングアップ中にエラーで失敗した場合の解決策を提供します。

*エラー：ウォーミングアップに失敗しました：`<website link>`*

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、すべての[&#x200B; サポートされているバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## イシュー

キャッシュのウォームアップに失敗しました。

<u>複製する手順</u>:

キャッシュウォームアップ操作を開始します。

<u>期待される結果</u>:

ページまたはサイト全体が読み込まれます。

<u>実際の結果</u>:

サイトが利用できないか、応答時間が長すぎます。 *エラー：ウォーミングアップに失敗しました：`<website link>`*

## 原因

HTTP アクセス制御が有効になっている場合、キャッシュ ウォームアップは機能しません。

## Solution

アクセス制御が有効になっていないことを確認します。特定のブランチ/環境に移動し、**設定** アイコンをクリックして、**HTTP アクセス制御**&#x200B;設定を確認します。このシナリオでは、キャッシュ ウォームアップを実行できず、アクセス制御を無効にする必要があります。

## 関連トピックス

* ユーザーガイドの[Adobe Commerce ユーザーガイド > フルページキャッシュ &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management#full-page-caching)。
* [&#x200B; キャッシュのウォーミングアップとサイトは、Adobe Commerce](/help/troubleshooting/miscellaneous/cache-warming-up-and-site-unavailable-on-magento.md)でサポート情報ベースで利用できません。
