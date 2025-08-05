---
title: Fastly キャッシングがクラウドインフラストラクチャのAdobe Commerceで機能しない
description: この記事では、サイトで Fastly キャッシュが機能しない問題の修正について説明します。 Fastly は、クラウドインフラストラクチャーのプランと実装に関するAdobe Commerceに含まれる CDN およびキャッシュサービスです。 Fastly 拡張機能が機能していることを確認したり、Fastly 拡張機能をデバッグしたりするには、curl コマンドを使用して特定の応答ヘッダーを表示します。 これらの応答ヘッダーの値は、Fastly が有効になっており、正しく機能しているかどうかを示します。 ヘッダーとキャッシュ動作の値に基づいて、問題をさらに調査できます。
exl-id: 725949e9-b69b-456f-9c56-e2163143a71e
feature: Cache, Cloud, Console, Paas
role: Developer
source-git-commit: 139c2836ba36686357c7a5458a36550c7b1273c1
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Fastly キャッシングがクラウドインフラストラクチャのAdobe Commerceで機能しない

この記事では、サイトで Fastly キャッシュが機能しない問題の修正について説明します。 Fastly は、クラウドインフラストラクチャーのプランと実装に関するAdobe Commerceに含まれる CDN およびキャッシュサービスです。 Fastly 拡張機能が機能していることを確認したり、Fastly 拡張機能をデバッグしたりするには、curl コマンドを使用して特定の応答ヘッダーを表示します。 これらの応答ヘッダーの値は、Fastly が有効になっており、正しく機能しているかどうかを示します。 ヘッダーとキャッシュ動作の値に基づいて、問題をさらに調査できます。

この情報は、ライブサイトおよびオリジンサーバーの Fastly ヘッダーを検証およびテストするのに役立ちます。

## 影響を受けるバージョン

* クラウドインフラストラクチャー上のAdobe Commerce
* Fastly 1.2.27 以降

## 問題

ライブサイト、実稼働、またはステージング環境では、キャッシュが機能していない可能性があります。

## 原因：

通常、Fastly のキャッシュが機能しない場合は、設定、資格情報が正しくない、サポートされていないAdobe Commerce拡張機能が問題になります。 Fastly を誤って設定した場合、またはサポートされていない拡張機能を使用してヘッダーを削除した場合、Fastly のキャッシュは機能しません。

## コマンドを使用したテストと応答ヘッダーの確認

### dig コマンドを使用したテスト

まず、URL に対して dig コマンドを使用してヘッダーを確認します。 ターミナルアプリケーションで、dig `<url>` と入力し、Fastly サービスがヘッダーに表示されることを確認します。 その他の dig テストについては、Fastly の [DNS 変更前のテスト ](https://docs.fastly.com/guides/basic-configuration/testing-setup-before-changing-domains) を参照してください。

例：

* ライブサイト：`dig http[s]://<your domain>`
* ステージング：`dig http[s]://staging.<your domain>.c.<instanceid>.ent.magento.cloud`
* 実稼動：`dig http[s]://<your domain>.{1|2|3}.<project ID>.ent.magento.cloud`

### curl コマンドによるテスト

次に、curl コマンドを使用して、X-Magento-Tags が存在することと、追加のヘッダー情報を確認します。 コマンドの形式は、ステージングと実稼動で異なります。

これらのコマンドについて詳しくは、`-H "host:URL"` を挿入する際に Fastly をバイパスし、接続場所（OneDrive スプレッドシートからの CNAME 情報）の元に置き換え、`-k` は SSL を無視し、詳細な応答を提供 `-v` ます。 ヘッダーが正しく表示される場合は、ライブサイトを確認して、ヘッダーを再度確認します。

* Fastly をバイパスしてオリジンサーバーに直接アクセスする際にヘッダーの問題が発生した場合は、コード、拡張機能、インフラストラクチャに問題がある可能性があります。
* オリジンサーバーに直接エラーが発生していないが、Fastly を通じてライブドメインにヘッダーが届いていない場合は、Fastly エラーが発生している可能性があります。

まず、**ライブサイト** を確認して、応答ヘッダーを検証します。 コマンドは、応答を受信するために Fastly 拡張機能を経由します。 正しいヘッダーが届かない場合は、オリジンサーバーを直接テストする必要があります。 このコマンドは、`Fastly-Magento-VCL-Uploaded` ヘッダーと `X-Cache` ヘッダーの値を返します。

1. ターミナルで、次のコマンドを入力してライブサイト URL をテストします。

   ```
   curl http://<live URL> -vo /dev/null -HFastly-Debug:1 [--resolve]
   ```

   ライブ URL が DNS で設定されておらず、静的ルートも設定されていない場合にのみ、`--resolve` を使用します。 例：

   ```
   curl http://www.mymagento.biz -vo /dev/null -HFastly-Debug:1
   ```

1. 応答ヘッダーを検証し、Fastly が機能していることを確認します。 このコマンドの出力は、curl のステージングおよび実稼動環境と似ています。 例えば、返される一意のヘッダーは、次のコマンドで確認できます。

   ```
   < Fastly-Magento-VCL-Uploaded: yes    < X-Cache: HIT, MISS
   ```

テストするには **ステージング** :

```
curl http[s]://staging.<your domain>.c.<instanceid>.ent.magento.cloud -H "host: <url>" -k -vo /dev/null -HFastly-Debug:1
```

**実稼動ロードバランサー** をテストするには：

```
curl http[s]://<your domain>.c.<project ID>.ent.magento.cloud -H "host: <url>" -k -vo /dev/null -HFastly-Debug:1
```

**実稼動オリジンノード** をテストするには：

```
curl http[s]://<your domain>.{1|2|3}.<project ID>.ent.magento.cloud -H "host: <url>" -k -vo /dev/null -HFastly-Debug:1
```

直接オリジンノード：

```
curl http[s]://<your domain>.{1|2|3}.<project ID>.ent.magento.cloud -H "host: <url>" -k -vo /dev/null -HFastly-Debug:1
```

例えば、公開 URL がwww.mymagento.bizの場合、次のようなコマンドを入力して実稼動サイトをテストします。

```
curl -k https://www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud -H 'Host: www.mymagento.biz' -vo /dev/null -HFastly-Debug:1
```

### 応答ヘッダーを確認

* 返された応答のヘッダーと値を確認します。
* Fastly-Magento-VCL-Uploaded が存在する必要があります
* X-Magento-Tags が返されます。
* Fastly-Module-Enabled は、Yes または Fastly 拡張機能バージョン番号のいずれかである必要があります
* X-Cache は HIT または HIT、HIT のいずれかである必要があります
* x-cache-hits は 1,1 にしてください
* キャッシュコントロール : max-age は 0 より大きくなければなりません
* プラグマはキャッシュする必要があります

次の例では、Pragma、X-Magento-Tags および Fastly-Module-Enabled の正しい値を示しています。

curl コマンドの出力は長くなる場合があります。 以下は概要に過ぎません。

```
* STATE: INIT => CONNECT handle 0x600057800; line 1402 (connection #-5000)
* Rebuilt URL to: https://www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud/
* Added connection 0. The cache now contains 1 members
* Trying 192.0.2.31...
* STATE: CONNECT => WAITCONNECT handle 0x600057800; line 1455 (connection #0)
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                             Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Connected to www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud (54.229.163.31) port 443 (#0)
* STATE: WAITCONNECT => SENDPROTOCONNECT handle 0x600057800; line 1562 (connection #0)
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* ALPN, offering h2

  ... portion omitted for brevity ...

< Set-Cookie: mage-messages=%5B%5D; expires=Wed, 22-Nov-2017 17:39:58 GMT; Max-Age=31536000; path=/
< Pragma: cache
< Expires: Wed, 23 Nov 2016 17:39:56 GMT
< Cache-Control: max-age=86400, public, s-maxage=86400, stale-if-error=5, stale-while-revalidate=5
< X-Magento-Tags: cb_welcome_popup store cb cb_store_info_mobile cb_header_promotional_bar cb_store_info cb_discount-promo-bar cpg_2 cb_83 cb_81 cb_84 cb_85 cb_86 cb_87 cb_88 cb_89 p5646 catalog_product p5915 p6040 p6197 p6227 p7095 p6109 p6122 p6331 p7592 p7651 p7690
< Fastly-Module-Enabled: yes
< Strict-Transport-Security: max-age=31536000
    < Content-Security-Policy: upgrade-insecure-requests
< X-Content-Type-Options: nosniff
< X-XSS-Protection: 1; mode=block
< X-Frame-Options: SAMEORIGIN
< X-Platform-Server: i-dff64b52
<
* STATE: PERFORM => DONE handle 0x600057800; line 1955 (connection #0)
* multi_done
  0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
* Connection #0 to host www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud left intact
```

## 解決

### Fastly-Module-Enabled がない

応答ヘッダーで Fastly-Module-Enabled に「yes」が表示されない場合は、Fasty モジュールがインストールされ、選択されていることを確認する必要があります。

ステージング環境と実稼動環境で Fastly が有効になっていることを確認するには、各環境のCommerce管理者で設定を確認します。

1. /admin 付きの URL （または変更した管理 URL）を使用して、ステージング環境および実稼動環境の Admin Console にログインします。
1. ストア/設定/詳細/システムに移動します。 スクロールして、「フルページキャッシュ」をクリックします。
1. Fastly CDN が選択されていることを確認します。
1. 「Fastly 設定」をクリックします。 Fastly サービス ID と Fastly API トークンが入力されていることを確認します（Fastly 資格情報）。 ステージング環境と実稼動環境に正しい資格情報が入力されていることを確認します。 「テスト資格情報」をクリックしてください。
1. composer.json を編集し、Fasty モジュールがバージョンに含まれていることを確認します。 このファイルには、バージョンと共にすべてのモジュールがリストされています。

   * 「require」セクションには、「fastly/magento2」が必要です。`<version number>`
   * 「リポジトリ」セクションには、次が必要です。

   ```
   "fastly-magento2": {    "type": "vcs",    "url": "https://github.com/fastly/fastly-magento2.git"    }
   ```

1. Configuration Management を使用する場合は、設定ファイルが必要です。 app/etc/config.app.php （2.0、2.1）またはapp/etc/config.php（2.2）ファイルを編集し、`'Fastly_Cdn' => 1` の設定が正しいことを確認します。 この設定は、`'Fastly_Cdn' => 0` （無効）にしないでください。Fastly を有効にした場合は、設定ファイルを削除し、bin/magento magento-cloud:scd-dump コマンドを実行して更新します。 このファイルの手順については、『設定ガイド』の [ システム固有の設定の管理例 ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html?lang=ja#manage-the-system-specific-configuration) を参照してください。

モジュールがインストールされていない場合は、[ 統合環境 ](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27242) ブランチにインストールし、ステージング環境と実稼動環境にデプロイする必要があります。 詳しくは、クラウドインフラストラクチャー上のCommerce ガイドの [Fastly の設定 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html?lang=ja) を参照してください。

### Fastly-Magento-VCL-Uploaded がありません

インストールおよび設定中に、Fastly VCL をアップロードしている必要があります。 これらは、作成したカスタム VCL スニペットではなく、Fastly モジュールによって提供される基本 VCL スニペットです。 Commerce手順については、『 Cloud Infrastructure ガイド』の [Fastly VCL スニペットのアップロード ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html?lang=ja#upload-vcl-to-fastly) を参照してください。

### X-Cache に MISS が含まれる

X-Cache が HIT、MISS または MISS、MISS の場合、同じ curl コマンドを再度入力して、ページが最近キャッシュから消去されていないことを確認します。

同じ結果が得られる場合は、curl コマンドを使用し、応答ヘッダーを確認します。

* プラグマはキャッシュ
* X-Magento-Tags が存在する
* キャッシュコントロール : max-age が 0 より大きい

問題が解決しない場合は、別の拡張機能がこれらのヘッダーをリセットしている可能性があります。 ステージングで次の手順を繰り返して、拡張機能を無効にし、問題を引き起こしている拡張機能を見つけます。 問題の原因となっている拡張機能を見つけたら、実稼動環境でその拡張機能を無効にする必要があります。

1. 拡張機能を無効にするには、Cloud Infrastructure ガイドのCommerceの [ 拡張機能の管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/extensions.html?lang=ja#manage-extensions) の節で説明されている手順に従ってください。
1. 拡張機能を無効にした後、**[!UICONTROL System]**/**[!UICONTROL Tools]**/**[!UICONTROL Cache Management]** に移動します。
1. 「**[!UICONTROL Flush Magento Cache]**」をクリックします。
1. ここで、一度に 1 つの拡張機能を有効にして、設定を保存し、キャッシュをフラッシュします。
1. curl コマンドを試して、応答ヘッダーを確認します。
1. 手順 4 と 5 を繰り返して、curl コマンドを有効にしテストします。 Fastly ヘッダーが表示されなくなった場合は、拡張機能が Fastly で問題を引き起こしていることがわかります。

Fastly ヘッダーをリセットしている拡張機能を分離する場合は、拡張機能の開発者に問い合わせてください。 サードパーティの拡張機能開発者に対して、Fastly キャッシュを使用するための修正やアップデートを提供することはできません。

## 詳しくは、開発者向けドキュメントを参照してください。

* [Fastly について ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/fastly.html?lang=ja)
* [Fastly のセットアップ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html?lang=ja)
* [ カスタム Fastly VCL スニペット ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets.html?lang=ja)
