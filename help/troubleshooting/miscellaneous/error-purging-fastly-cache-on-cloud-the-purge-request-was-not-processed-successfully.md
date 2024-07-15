---
title: クラウド上の Fastly キャッシュをパージする際にエラーが発生しました（パージリクエストが正常に処理されませんでした）
description: 「この記事では、Fastly パージオプションを使用し、「パージリクエストが正常に処理されませんでした」というエラーが表示された場合の修正方法を説明します。」 Fastly は、クラウドインフラストラクチャーのプランと実装に関するAdobe Commerceに含まれる CDN およびキャッシュサービスです。 Fastly パージオプションを使用しようとして、処理されない場合、環境に間違った Fastly 資格情報が存在するか、問題が発生した可能性があります。'
exl-id: 568b1f4c-2ccb-4740-a6e4-d227a55fcfe6
feature: Cache, Cloud, Paas
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# クラウド上の Fastly キャッシュをパージする際にエラーが発生しました（パージリクエストが正常に処理されませんでした）

この記事では、Fastly パージオプションを使用し、「*パージリクエストが正常に処理されませんでした* というエラーが表示される場合の修正方法を説明します。 Fastly は、クラウドインフラストラクチャーのプランと実装に関するAdobe Commerceに含まれる CDN およびキャッシュサービスです。 Fastly のパージオプションを使用しようとして、処理されない場合、環境に間違った Fastly 資格情報が存在するか、問題が発生した可能性があります。

この情報は、ライブサイトおよびオリジンサーバーの Fastly ヘッダーを検証およびテストするのに役立ちます。

## 影響を受けるバージョン

* クラウドインフラストラクチャー 2.1.X 以降でのAdobe Commerce
* Fastly 1.2.27 以降

## 問題

キャッシュは機能していますが、パージしようとすると、エラーが発生するか、機能しません。 エラーには、「パージリクエストが正常に処理されませんでした」と含まれます。

## 原因：

お使いの環境に設定されている認証情報が正しくないか、VCL スニペットのアップロードが必要な場合があります。

## 解決

### Fastly 資格情報を確認

お使いの環境に正しい Fastly サービス ID と API トークンがあるかどうかを確認します。 実稼動環境にステージング資格情報がある場合、パージが正しく処理されないか、正しく処理されない可能性があります。

1. 管理者として、ローカルのCommerce管理者にログインします。
1. **ストア**/設定/**設定**/**詳細**/**システム** をクリックし、「**フルページキャッシュ**」を展開します。    ![magento_full_page_cache_2.4.1.png](assets/magento_full_page_cache_2.4.1.png)
1. Fastly 設定を展開し、お使いの環境の Fastly サービス ID と API トークンを確認します。
1. 値を変更する場合は、「認証情報をテスト」をクリックします。

### VCL スニペットのチェック

資格情報が正しい場合、VCL に問題がある可能性があります。 サービスごとに VCL を一覧表示および確認するには、ターミナルで次の API 呼び出しを入力します。

```
curl -X GET -s https://api.fastly.com/service/<Service ID>/version/<Editable Version #>/snippet -H "Fastly-Key:FASTLY_API_TOKEN"
```

VCL のリストを確認します。 Fastly のデフォルト VCL に問題がある場合は、再度アップロードするか、[Fastly のデフォルト VCL](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets) に従ってコンテンツを確認することができます。 Commerce カスタム VCL の編集については、『 Cloud Infrastructure ガイド』の [ カスタム Fastly VCL スニペット ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets.html) を参照してください。

## 詳細情報

開発者向けドキュメントでは、

* [Fastly について ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/fastly.html)
* [Fastly のセットアップ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html)
* [ カスタム Fastly VCL スニペット ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets.html)
