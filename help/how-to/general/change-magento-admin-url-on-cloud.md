---
title: クラウドインフラストラクチャー上のAdobe Commerceの管理者 URL の変更
description: デフォルトでは、[Commerce管理者 ] （https://docs.magento.com/m2/ee/user_guide/stores/admin.html）の URL は*&lt;domain\_name&gt;/admin*に設定されています。 この記事では、URL を変更する方法を説明します。
exl-id: 6236370c-e0a2-45a6-a38f-12e219c540af
feature: Admin Workspace, Cloud
source-git-commit: 04dba4e2adeaaa7649b817444024bf96e7830ad3
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceの管理者 URL の変更

デフォルトでは、[Commerce Admin](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/admin.html) の URL は *&lt;domain\_name>/admin* に設定されています。 この記事では、URL を変更する方法を説明します。

## 方法 1：管理者を使用して変更する

ユーザーガイドの手順 [ カスタム管理者 URL の使用/管理者からの変更 ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html#use-a-custom-admin-url) をお読みください。

## 方法 2:ADMIN\_URL 環境変数を追加する

### 統合環境

[Cloud Console](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html) から、次の設定で新しい変数を追加します。

**名前：** ADMIN\_URL **値：** 新しい管理者 URL

* 詳しい手順については、開発者向けドキュメントの [ 環境変数の追加 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment) を参照してください。
* 開発者向けドキュメントの [ 環境変数 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-admin.html) も参照してください。

### Cloud Console でステージング環境と実稼動環境が使用できない場合

[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) ステージング環境または実稼動環境の ADMIN\_URL 変数の追加をリクエストします。

Cloud Console からステージングおよび実稼動にアクセスできる場合は、前述の *統合環境* の節で説明したように、環境変数を追加します。

### Cloud CLI を使用した変数の追加

次の Cloud CLI コマンド（メイン用）を使用して、ADMIN\_URL 変数を追加できます。

`magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master --inheritable false`

手順について詳しくは、『 Cloud Infrastructure ガイド』のCommerceの管理変数に関するトピックの [ 管理者 URL の変更 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-admin.html?lang=en#change-the-admin-url) を参照してください。

Cloud CLI を使用して ADMIN\_URL 変数を変更すると、環境の再デプロイがトリガーされることに注意してください。 変数は、デフォルトで継承可能です。継承を防ぐには、Cloud CLI コマンドオプションを使用して、変数の値を子環境に継承しないことを指定します。 Cloud Infrastructure ガイドのCommerceの変数レベルのトピック [ 表示 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/variable-levels.html#visibility) を参照してください。
