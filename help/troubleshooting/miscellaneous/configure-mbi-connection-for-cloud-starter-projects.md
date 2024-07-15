---
title: 既存の Cloud Starter プロジェクトへのAdobe Commerce Intelligence接続の設定
description: この記事では、既存の Cloud Starter プロジェクトにAdobe Commerce Intelligence接続を設定する場合の解決策を説明します。
feature: Commerce Intelligence
role: Developer
exl-id: 56f6ad64-729d-4e3a-93a9-da1b91bc5c1d
source-git-commit: b75328202952bf4c8f57ddc538b5c9e4318b2001
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# 既存の Cloud Starter プロジェクトへのAdobe Commerce Intelligence接続の設定

>[!NOTE]
>
>Adobe Commerce Intelligenceは、以前はMagento Business Intelligence（MBI）と呼ばれていました。

この記事では、既存の Cloud Starter プロジェクトにAdobe Commerce Intelligence接続を設定する場合の解決策を説明します。

## 影響を受ける製品とバージョン

cloud starter 上のAdobe Commerce（すべてのバージョン）

## 問題

既存の Cloud Starter プロジェクトのCommerce Intelligence接続を設定する。

>[!NOTE]
>
>Adobeでは、新しい Cloud Starter サブスクリプションをサポートしなくなりましたが、既存のスタータープロジェクトがある場合は、以下の手順に従って接続を設定する必要があります。

## 解決策

Cloud Starter プロジェクトのCommerce Intelligenceをアクティブ化するには、Commerce Intelligence アカウントを作成し、SSH キーを作成して、最後にAdobe Commerce データベースに接続します。

次の手順に従います。

1. Adobe Commerce Intelligence アカウントを作成します。

   * [accounts.magento.com/customer/account/login](https://account.magento.com/customer/account/login) に移動します。
   * **[!UICONTROL My Account]**/**[!UICONTROL My MBI Instances]** に移動します。
   * **[!UICONTROL Create Instance]** をクリックします。 このボタンが表示されない場合は、カスタマーサクセスマネージャーまたはカスタマーテクニカルアドバイザーにお問い合わせください。
   * Cloud Starter サブスクリプションを選択します。 Cloud Starter のサブスクリプションのみを持っている場合は、これが自動的に選択されます。
   * 「**[!UICONTROL Continue]**」をクリックします。
   * アカウントを作成するには、情報を入力します。

   ![MBI アカウントの作成 ](/help/troubleshooting/miscellaneous/assets/create_mbi_account.png)

   * インボックスに移動し、メールアドレスを確認します。

   ![ メールアドレスを確認 ](/help/troubleshooting/miscellaneous/assets/verify_email_address_mbi.png)

   * パスワードを作成します。

   ![ パスワードの作成 ](/help/troubleshooting/miscellaneous/assets/create_password_mbi.png)

   * アカウントを作成したら、新しいアカウントにユーザーを追加するオプションがあります。 次の手順を実行するために、テクニカル管理者を追加できるようになりました。

   ![ ユーザーを追加 ](/help/troubleshooting/miscellaneous/assets/add_users_mbi.png)

1. ストアに関する情報を入力して、環境設定を指定します。

   ![ ストア情報の追加 ](/help/troubleshooting/miscellaneous/assets/add_store_info_mbi.png)

   オンボーディングフローの 3 番目の手順でデータベースを接続する前に、収集する必要がある情報がいくつかあります。 手順 9 の *[!UICONTROL Connect your database]* ページに入力します。

1. 専用のCommerce Intelligence ユーザーを作成します。

   * [account.adobe.com](https://account.adobe.com/) に新しいユーザーを作成します。
   * [https://accounts.magento.com/customer/account/](https://accounts.magento.com/customer/account/) に移動して、Adobe Commerce アカウントを生成します。
   * 新しいユーザーを使用する理由 Adobe Commerce IntelligenceでアカウントのCommerce Intelligence data warehouse に転送される新しいデータを継続的に取得するには、ユーザーをプロジェクトに追加する必要があります。 このユーザーは、その接続として機能します。 このユーザーをプロジェクトに追加する場合は、手順 4 を参照してください。
   * 専用のCommerce Intelligence ユーザーを用意する理由は、追加されたユーザーが誤ってディアクティベートまたは削除されてCommerce Intelligence接続が停止するのを防ぐためです。

1. 新しく作成したユーザーを *コントリビューター* としてプロジェクトのプライマリ環境に追加します。

   ![ コントリビューターとしてユーザーを追加 ](/help/troubleshooting/miscellaneous/assets/contributor_user_mbi.png)

1. Commerce Intelligenceの SSH キーを入手します。

   * Commerce Intelligenceのセットアップユーザーインターフェイスの「**[!UICONTROL Connect your database]**」ページに移動し、下にスクロールして「**[!UICONTROL Encryption settings]**」を選択します。
   * フィールド **[!UICONTROL Encryption Type]** に「**[!UICONTROL SSH Tunnel]**」を選択します。
   * ドロップダウンから、指定したMagento BI Essentials 公開鍵をコピー&amp;ペーストできます。

   ![ 暗号化設定 ](/help/troubleshooting/miscellaneous/assets/encryption_type_mbi.png)

1. 手順 5 で作成したCommerce Intelligence ユーザーに、新しいMagentoBI Essentials 公開鍵を追加します。

   * [accounts.magento.com/customer/account/login](https://account.magento.com/customer/account/login) に移動します。 作成した新しいCommerce Intelligence ユーザーのアカウントのログイン情報でログインします。 次に、「**[!UICONTROL Account Settings]**」タブに移動します。
   * ページを下にスクロールし、「SSH キー」のドロップダウンを展開します。 次に、「**[!UICONTROL Add a public key]**」をクリックします。

   ![ 公開鍵を追加 ](/help/troubleshooting/miscellaneous/assets/add_public_key_mbi.png)

   * 上記のMagento MBI Essentials SSH 公開鍵を追加します。

   ![SSH 公開鍵の追加 ](/help/troubleshooting/miscellaneous/assets/add_ssh_key_mbi.png)

1. Business Intelligenceに必要な MySQL 資格情報を入力します。

   * `.magento/services.yaml` を更新します。

   ```
   mysql:
    type: mysql:10.0
    disk: 2048
    configuration:
        schemas:
            - main
        endpoints:
            mysql:
                default_schema: main
                privileges:
                    main: admin
            mbi:
                default_schema: main
                privileges:
                    main: ro
   ```

   * `.magento.app.yaml` を更新します。

   ```
   relationships:
            database: "mysql:mysql"
            mbi: "mysql:mbi"
            redis: "redis:redis"
   ```

1. データベースのCommerce Intelligenceへの接続に関する情報を取得します。

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp` を実行して、データベースの接続に関する情報を取得します。

   次の出力のような情報が表示されます。

   ```
   "mbi" : [
              {
                 "scheme" : "mysql",
                 "rel" : "mbi",
                 "cluster" : "vfbfui4vmfez6-master-7rqtwti",
                 "query" : {
                    "is_master" : true
                 },
                 "ip" : "169.254.169.143",
                 "path" : "main",
                 "host" : "mbi.internal",
                 "hostname" : "3m7xizydbomhnulyglx2ku4wpq.mysql.service._.magentosite.cloud",
                 "username" : "mbi",
                 "service" : "mysql",
                 "port" : 3306,
                 "password" : "[password]"
              }
           ],
   ```

1. Adobe Commerce データベースに接続します。

   ![Adobe Commerce データベースに接続する ](/help/troubleshooting/miscellaneous/assets/connect_magento_database_mbi.png)

   *入力*:

   * 統合名：[ 統合の名前を選択します。]
   * ホスト：`mbi.internal`
   * ポート：3306
   * ユーザー名：mbi
   * パスワード：[ 手順 8 の出力で指定したパスワードを入力します。]
   * データベース名：メイン
   * テーブル接頭辞：[ テーブル接頭辞がない場合は、空白のままにします ]

1. [!UICONTROL Timezone Settings] を設定します。

   ![ タイムゾーン設定 ](/help/troubleshooting/miscellaneous/assets/timezone_settings_mbi.png)

   *入力*

   * データベース：タイムゾーン：UTC
   * 目的のタイムゾーン：[ データを表示するタイムゾーンを選択します。]

1. 暗号化設定に関する情報を取得します。

   * プロジェクト UI には SSH アクセス文字列を指定します。 この文字列は、**[!UICONTROL Encryption settings]** の設定でリモートアドレスとユーザー名に必要な情報を収集するために使用できます。 「**[!UICONTROL SSH]**」を選択して、ユーザー名とリモートアドレスを確認します。 *@* の前のテキスト文字列はユーザー名で、*@* の後のテキスト文字列はリモートアドレスです。

   ![ サイトマスターへのアクセス ](/help/troubleshooting/miscellaneous/assets/access_site_mbi.png)

1. [!UICONTROL Encryption Settings] の情報を入力します。

   ![ 暗号化設定 ](/help/troubleshooting/miscellaneous/assets/encryption_type_mbi.png)

   *入力*

   * 暗号化の種類：SSH トンネル
   * リモートアドレス：ssh.us-3.magento.cloud
   * ユーザー名：vfbfui4vmfez6-master-7rqtwti—mymagento
   * ポート：22

1. 「**[!UICONTROL Save Integration]**」をクリックします。
1. これで、Commerce Intelligence Essentials アカウントに正常に接続されました。
1. Adobe Commerce Intelligence Pro をご利用のお客様は、カスタマーサクセスマネージャーまたはカスタマーテクニカルアドバイザーに連絡して、次の手順を調整してください。
