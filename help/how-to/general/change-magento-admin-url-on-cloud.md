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

デフォルトでは、 [Commerce管理者](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/admin.html) URL はに設定されています。 *&lt;domain _name=&quot;&quot;>/admin*. この記事では、URL を変更する方法を説明します。

## 方法 1：管理者を使用して変更する

手順を読みます。 [カスタム管理者 URL の使用/管理者から変更](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html#use-a-custom-admin-url) を参照してください。

## 方法 2:ADMIN\_URL 環境変数を追加する

### 統合環境

から [クラウドコンソール](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html)で、次の変数を新たに追加します。

**名前：** ADMIN\_URL **値：** 新しい管理者 URL

* 詳細な手順については、を参照してください [環境変数の追加](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment) 開発者向けドキュメントを参照してください。
* も参照してください。 [環境変数](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-admin.html) 開発者向けドキュメントを参照してください。

### Cloud Console でステージング環境と実稼動環境が使用できない場合

[サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) ステージング環境または実稼動環境用の ADMIN\_URL 変数の追加をリクエストします。

Cloud Console からステージングおよび実稼動にアクセスできる場合は、の説明に従って、環境変数を追加します *統合環境* 上記の節

### Cloud CLI を使用した変数の追加

次の Cloud CLI コマンド（メイン用）を使用して、ADMIN\_URL 変数を追加できます。

`magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master --inheritable false`

詳しい手順については、次を参照してください [管理者 URL の変更](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-admin.html?lang=en#change-the-admin-url) Cloud Infrastructure ガイドのCommerceの「管理変数」トピックで、次の操作を行います。

Cloud CLI を使用して ADMIN\_URL 変数を変更すると、環境の再デプロイがトリガーされることに注意してください。 変数は、デフォルトで継承可能です。継承を防ぐには、Cloud CLI コマンドオプションを使用して、変数の値を子環境に継承しないことを指定します。 を参照してください。 [可視性](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/variable-levels.html#visibility) cloud Infrastructure ガイドのCommerceの変数レベルに関するトピック。
