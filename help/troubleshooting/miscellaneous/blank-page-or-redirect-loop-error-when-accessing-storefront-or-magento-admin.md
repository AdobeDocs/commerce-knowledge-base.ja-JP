---
title: ストアフロントまたはCommerce管理者にアクセスする際に、空白ページまたはリダイレクトループエラーが発生する
description: この記事では、Adobe Commerce ストアフロントまたはバックエンドにアクセスすると、空白のページまたはリダイレクトループが発生した場合の問題の解決策を説明します。
exl-id: 65869de2-1939-481b-844b-69122345b407
feature: Admin Workspace, Cache, Storefront
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# ストアフロントまたはCommerce管理者にアクセスする際に、空白ページまたはリダイレクトループエラーが発生する

この記事では、Adobe Commerce ストアフロントまたはバックエンドにアクセスすると、空白のページまたはリダイレクトループが発生した場合の問題の解決策を説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン
* Adobe Commerce オンプレミス、すべてのバージョン
* Magento Open Source、すべてのバージョン

## 問題

<u> 再現手順 </u>

ストアフロントまたは管理ページを開きます。

<u> 期待される結果 </u>

ページが開きます。

<u> 実際の結果 </u>

ページが空白になるか、「この Web ページにはリダイレクトループがあります *というエラーメッセージが表示* れます。

## 原因：

この問題を発生させる最も考えられる理由の 1 つは、Adobe Commerceが保護されていない URL から保護された URL にリダイレクトするように設定されているものの、保護されていない URL は保護された URL 設定の値として指定されることです。

この問題を修正するには、セキュアリンクの値を修正する必要があります。

## 解決策

これが問題の原因であることを確認するには、次の手順に従います。

1. `'core_config_data'` DB テーブルの `web/secure/enable_upgrade_insecure`、`web/secure/use_in_adminhtml` （管理者に空白/ループリダイレクトの問題がある場合）または `web/secure/use_in_frontend` （ストアフロントに空白/ループリダイレクトの問題がある場合）の値を確認します。
   * `web/secure/enable_upgrade_insecure` を「1」に設定すると、Adobe Commerceは応答ヘッダー `Content-Security-Policy: upgrade-insecure-requests` を追加するように設定されます。これにより、ブラウザーは HTTPS を使用して、HTTP を経由するすべてのクエリをリダイレクトするようになります
https （管理者とストアフロントの両方について）
   * `web/secure/use_in_adminhtml` を「1」に設定すると、Adobe Commerceは、管理ページのすべての HTTP リクエストに対して HTTPS リダイレクトを返します。
   * `web/secure/use_in_frontend` を「1」に設定すると、Adobe Commerceは、ストアフロントページのすべての HTTP リクエストに対して HTTPS リダイレクトを返します。
1. `'core_config_data'` テーブルの `web/secure/base_url` と `web/unsecure/base_url` の値を確認します。 両方の言語が次の語句で始まる場合    `http` の後、「安全な」値を修正する必要があります。

問題の修正：

1. `web/secure/base_url.` に `https` で始まる値を設定します
1. 変更を適用するには、次のコマンドを実行して、設定キャッシュをクリーンアップします。

   ```bash
   php <your_magento_install_dir>/bin/magento cache:clean config
   ```

## 関連資料

Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
