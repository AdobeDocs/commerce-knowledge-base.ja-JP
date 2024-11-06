---
title: Adobe Commerce Fastly に関するトラブルシューティング
description: このAdobe Commerce ユーザー向け Fastly トラブルシューティングツールでは、表示される症状に対する回答に基づいて、ソリューションを紹介します。 質問をクリックして、次のオプションまたは回答を表示します。
exl-id: c5c51b89-5a7d-49ba-a0ee-7abbaf78fdad
feature: Support, Services
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Adobe Commerce Fastly に関するトラブルシューティング

このAdobe Commerce ユーザー向け Fastly トラブルシューティングツールでは、表示される症状に対する回答に基づいて、ソリューションを紹介します。 質問をクリックして、次のオプションまたは回答を表示します。

## 手順 1 - Fastly サービスの検証 {#step-1}

+++**お客様から Fastly に関する問題が報告された。 Fastly のサービスは停止していますか？**

a.はい – [Fastly サービスステータス ](https://status.fastly.com/) を確認し、[Adobe Commerce サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) ます。\
b.いいえ – [ 手順 2](#step-2) に進みます。

+++

## 手順 2 - VCL 構成ファイルのチェック {#step-2}

+++**バックエンドテスターを実行すると、エラーが発生しますか？**

[ バックエンドテスター – Fastly](https://magento-tester.global.ssl.fastly.net/magento-tester/) を使用してプロジェクト URL を実行します。 ページがキャッシュ可能な場合は、VCL 設定ファイルのバージョン、Fastly モジュールのバージョン、その他の便利なトラブルシューティング情報が表示されます。 何か間違いがありますか。

a.はい。メッセージが表示されます _プラグイン VCL バージョンが古くなっています！ 再アップロードしてください。_ このエラーの解決策については、[Fastly エラー：プラグイン VCL のバージョンが古くなっています。 再アップロードしてください ](/help/troubleshooting/miscellaneous/fastly-error-plugin-vcl-version-is-outdated-please-re-upload.md)..\
b.いいえ – [ 手順 3](#step-3)。

+++

## 手順 3 – 画像の最適化エラーを確認する {#step-3}

+++**画像の最適化エラー？**

a.はい – [ 画像の最適化を有効にする際にエラーが発生します ](/help/troubleshooting/miscellaneous/error-enabling-image-optimization-in-magento-commerce.md)。\
b.いいえ – CLI/ターミナルで実行して、DNS を確認します：`dig [your website.com] + short`。 [ 手順 4](#step-4) に進みます。

+++

## 手順 4 - DNS の検証 {#step-4}

+++**`dig` を実行するとどうなりますか？**

`dig` を実行すると、prod.magentocloud.map.fastly.netまたは次のいずれかの IP アドレスを指すレコードが返されませんでした（開発者向けドキュメントの [ 実稼動設定で DNS 設定を更新 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist#update-dns-configuration-with-production-settings) を参照してください）。

* 151.101.1.124
* 151.101.65.124
* 151.101.129.124
* 151.101.193.124

a.はい。この問題は DNS に関連するものではありません。 [ 手順 5](#step-5) に進みます。\
b.いいえ – 問題は DNS に関連している可能性があります。 お客様は [DNS 構成を確認 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist#update-dns-configuration-with-production-settings) するか、DNS プロバイダに詳細を問い合わせる必要があります。

+++

## 手順 5 – 接続の確認 {#step-5}

+++**CLI/ターミナルで `curl -svo /dev/null "https://website.com"` を実行すると、「Connection Insecure」または「Not Secure」というメッセージが返されますか？**

a.はい – 証明書の問題である可能性があります。 ブラウザーで web サイトにアクセスし、ロックアイコンを選択して、証明書の有効期限を探します。 [ 手順 6](#step-6) に進みます。\
b.いいえ。[http://fastly-debug.com](https://www.fastly-debug.com/) にアクセスして、この情報を [Adobe Commerce サポートチケット ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) で共有します。

+++

## 手順 6 – 有効な TSL 証明書があることを確認する {#step-6}

+++**証明書の有効期限が切れていますか？**

回答：はい。認証局（CA）で TLS 証明書を更新する必要があります。\
b.いいえ – 証明書がまったくない場合があります。 Adobe Commerceをお持ちの場合は、TLS 証明書を購入することをお勧めします。 クラウドインフラストラクチャー上でAdobe Commerceを使用している場合は、ドメイン検証済みの Let&#39;s Encrypt SSL/TLS 証明書を用意して、Fastly から安全な HTTPS トラフィックを提供できます。 開発者向けドキュメントの [SSL/TLS 証明書のプロビジョニング ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#provision-ssltls-certificates) を参照してください。

+++

[手順 1 に戻る](#step-1)
