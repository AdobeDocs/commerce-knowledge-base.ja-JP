---
title: Adobe Commerce Fastly に関するトラブルシューティング
description: このAdobe Commerce ユーザー向け Fastly トラブルシューティングツールでは、表示される症状に対する回答に基づいて、ソリューションを紹介します。 質問をクリックして、次のオプションまたは回答を表示します。
exl-id: c5c51b89-5a7d-49ba-a0ee-7abbaf78fdad
feature: Support, Services
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Adobe Commerce Fastly に関するトラブルシューティング

このAdobe Commerce ユーザー向け Fastly トラブルシューティングツールでは、表示される症状に対する回答に基づいて、ソリューションを紹介します。 質問をクリックして、次のオプションまたは回答を表示します。

## 手順 1 - Fastly サービスの検証 {#step-1}

+++**お客様から Fastly に関する問題が報告される。 Fastly のサービスはダウンしていますか？**

a.はい – 確認 [Fastly サービスステータス](https://status.fastly.com/)、および [Adobe Commerce サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).\
b.いいえ – に進みます。 [手順 2](#step-2).

+++

## 手順 2 - VCL 構成ファイルのチェック {#step-2}

+++**バックエンドテスターを実行するとエラーが発生しますか？**

からプロジェクト URL を実行 [バックエンドテスター – Fastly](https://magento-tester.global.ssl.fastly.net/magento-tester/). ページがキャッシュ可能な場合は、VCL 設定ファイルのバージョン、Fastly モジュールのバージョン、その他の便利なトラブルシューティング情報が表示されます。 何か間違いがありますか。

a.はい – メッセージは届いています _プラグイン VCL のバージョンが古くなっています。 再アップロードしてください。_ このエラーの解決策については、次を参照してください [Fastly エラー：プラグイン VCL のバージョンが古くなっています。 再アップロードしてください](/help/troubleshooting/miscellaneous/fastly-error-plugin-vcl-version-is-outdated-please-re-upload.md).\
b.いいえ –  [手順 3](#step-3).

+++

## 手順 3 – 画像の最適化エラーを確認する {#step-3}

+++**画像の最適化エラー？**

a.はい –  [画像の最適化を有効にする際にエラーが発生する](/help/troubleshooting/miscellaneous/error-enabling-image-optimization-in-magento-commerce.md).\
b.いいえ – CLI/ターミナルでを実行して、DNS を確認します。 `dig [your website.com] + short`. 次の手順に進みます。 [手順 4](#step-4).

+++

## 手順 4 - DNS の検証 {#step-4}

+++**実行時の動作 `dig`?**

実行したとき `dig` prod.magentocloud.map.fastly.netまたは次のいずれかの IP アドレスを指すレコードを返しましたか（ [実稼働設定で DNS 設定を更新します](https://devdocs.magento.com/cloud/live/site-launch-checklist.html#dns) 開発者向けドキュメントで）:

* 151.101.1.124
* 151.101.65.124
* 151.101.129.124
* 151.101.193.124

a.はい。この問題は DNS に関連するものではありません。 次の手順に進みます。 [手順 5](#step-5).\
b.いいえ – 問題は DNS に関連している可能性があります。 顧客は、 [dns 設定を確認](https://devdocs.magento.com/cloud/live/site-launch-checklist.html#dns "https://devdocs.magento.com/cloud/live/site-launch-checklist.html#dns") または、DNS プロバイダーに問い合わせてください。

+++

## 手順 5 – 接続の確認 {#step-5}

+++**実行中に「Connection Insecure」または「Not Secure」というメッセージが返される `curl -svo /dev/null "https://website.com"` CLI/ターミナルで実行しますか。**

a.はい – 証明書の問題である可能性があります。 ブラウザーで web サイトにアクセスし、ロックアイコンを選択して、証明書の有効期限を探します。 次の手順に進みます。 [手順 6](#step-6).\
ロ。いいえ – 訪問 [http://fastly-debug.com](https://www.fastly-debug.com/) この情報をで共有する [Adobe Commerce サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

## 手順 6 – 有効な TSL 証明書があることを確認する {#step-6}

+++**証明書の有効期限が切れていますか？**

回答：はい。認証局（CA）で TLS 証明書を更新する必要があります。\
b.いいえ – 証明書がまったくない場合があります。 Adobe Commerceをお持ちの場合は、TLS 証明書を購入することをお勧めします。 クラウドインフラストラクチャー上でAdobe Commerceを使用している場合は、ドメイン検証済みの Let&#39;s Encrypt SSL/TLS 証明書を用意して、Fastly から安全な HTTPS トラフィックを提供できます。 参照： [ssl/TLS 証明書のプロビジョニング](https://devdocs.magento.com/cloud/cdn/configure-fastly.html#provision-ssltls-certificates) 開発者向けドキュメントを参照してください。

+++

[手順 1 に戻る](#step-1)
