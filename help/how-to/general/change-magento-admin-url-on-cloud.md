---
title: クラウドインフラストラクチャー上のAdobe Commerceの管理者 URL の変更
description: デフォルトでは、[Commerce管理者 ] （https://experienceleague.adobe.com/ja/docs/commerce-admin/start/admin/admin）の URL は*&lt;domain_name&gt;/admin*に設定されています。 この記事では、URL を変更する方法を説明します。
exl-id: 6236370c-e0a2-45a6-a38f-12e219c540af
feature: Admin Workspace, Cloud
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceの管理者 URL の変更

デフォルトでは、[Commerce Admin](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/admin.html?lang=ja) の URL は *&lt;domain\_name>/admin* に設定されています。 この記事では、URL を変更する方法を説明します。

## 方法 1：管理者を使用して変更する

ユーザーガイドの手順 [&#x200B; カスタム管理者 URL の使用/管理者からの変更 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html?lang=ja#use-a-custom-admin-url) をお読みください。

## 方法 2:ADMIN\_URL 環境変数を追加する

### 統合環境

[Cloud Console](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html?lang=ja) から、次の設定で新しい変数を追加します。

**名前：** ADMIN\_URL **値：** 新しい管理者 URL

* 詳しい手順については、開発者向けドキュメントの [&#x200B; 環境変数の追加 &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html?lang=ja#configure-environment) を参照してください。
* 開発者向けドキュメントの [&#x200B; 環境変数 &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-admin.html?lang=ja) も参照してください。

### Cloud Console でステージング環境と実稼動環境が使用できない場合

[&#x200B; サポートチケットを送信 &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) ステージング環境または実稼動環境の ADMIN\_URL 変数の追加をリクエストします。

Cloud Console からステージングおよび実稼動にアクセスできる場合は、前述の *統合環境* の節で説明したように、環境変数を追加します。

### Cloud CLI を使用した変数の追加

次の Cloud CLI コマンド（メイン用）を使用して、ADMIN\_URL 変数を追加できます。

`magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master --inheritable false`

手順について詳しくは、『 Cloud Infrastructure ガイド』のCommerceの管理変数に関するトピックの [&#x200B; 管理者 URL の変更 &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-admin.html?lang=ja#change-the-admin-url) を参照してください。

Cloud CLI を使用して ADMIN\_URL 変数を変更すると、環境の再デプロイがトリガーされることに注意してください。 変数は、デフォルトで継承可能です。継承を防ぐには、Cloud CLI コマンドオプションを使用して、変数の値を子環境に継承しないことを指定します。 Cloud Infrastructure ガイドのCommerceの変数レベルのトピック [&#x200B; 表示 &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/variable-levels.html?lang=ja#visibility) を参照してください。
