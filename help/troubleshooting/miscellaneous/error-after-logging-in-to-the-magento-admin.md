---
title: Commerce Adminにログインした後にエラーが発生する
description: この記事では、要求されたURLがこのサーバーに見つからないというエラーメッセージが表示される問題の解決策を提供します。
exl-id: f52b383b-87f2-4216-9bf4-e765db31ca6b
feature: Admin Workspace
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: bb2df8be-afdd-4818-b6b5-95ca1dd3bc3a
    internal-label: Admin workspace
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%
---
# Commerce Adminにログインした後にエラーが発生する

この記事では、要求されたURLがこのサーバーに見つからないというエラーメッセージが表示される問題の解決策を提供します。

## 詳細

要求されたURL /magento2index.php/admin/admin/dashboard/index/key/0c81957145a968b697c32a846598dc2e/がこのサーバーに見つかりませんでした。

URLの`magento2`と`index.php`の間にスラッシュ文字がないことを確認してください。

## Solution

ベース URLが正しくありません。 ベース URLは次のようにする必要があります。

* `http://`または`https://`で始める
* スラッシュで終わる（`/`）
* `core_config_data` データベーステーブルの`web/unsecure/base_url` レコードの大文字と小文字を一致させます

有効な値を使用してインストールを再実行します。

## 関連トピックス

[Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
