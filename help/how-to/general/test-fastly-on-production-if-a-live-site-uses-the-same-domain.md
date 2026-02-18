---
title: 実稼働サイトで同じドメインを使用している場合は、実稼動環境で Fastly をテストします
description: 実稼動ドメイン（「example.com」）で稼働中のサイトがあり、クラウドインフラストラクチャの実稼動環境で Fastly CDN を有効にしてAdobe Commerceで新しいストアをテストする必要がある場合は、ローンチ前のテストアクティビティには、以前に Fastly に追加したサブドメイン（「prod.example.com」など）を使用することをお勧めします。 この記事では、詳細を説明し、関連するAdobe Commerce ドキュメントリソースへの便利なリンクを提供します。
exl-id: bc9d11c8-ce47-461d-b5b8-c03494bc4ceb
feature: Cache
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# 実稼働サイトで同じドメインを使用している場合は、実稼動環境で Fastly をテストします

実稼動ドメイン（`example.com`）で稼働中のサイトがあり、クラウドインフラストラクチャの実稼動環境で Fastly CDN を有効にしてAdobe Commerce上の新しいストアをテストする必要がある場合は、起動前のテストアクティビティには、以前 Fastly に追加したサブドメイン（`prod.example.com` など）を使用することをお勧めします。 この記事では、詳細を説明し、関連するAdobe Commerce ドキュメントリソースへの便利なリンクを提供します。

## 問題

`example.com` の実稼動ドメインを使用する現在のストアは、稼働中です。 ただし、クラウドインフラストラクチャ上にAdobe Commerceを使用して構築し、Fastly フルページキャッシュサービスを有効にして実稼動環境にデプロイした、新しいストアをテストする必要があります。

問題は、クラウドインフラストラクチャプロジェクト上のAdobe Commerceの実稼動環境で同じライブドメイン（`example.com`）が使用されており、新しいサイトをこのドメインに切り替えると、現在のライブストアが同じドメインで動作するようになります。

### Fastly を実稼動環境でのテストに使用する理由

理論的には、Fastly CDN の使用をスキップし、フルページキャッシュを有効にせずに、実稼動環境のクラウドインフラストラクチャストアでAdobe Commerceをテストすることができます。

ただし、フルページキャッシュを有効にすると、ストアのパフォーマンスが異なります。起動前に CDN でテストしていない場合、サイトの実際のライブパフォーマンスがわかりません。 Fastly CDN を有効にした実稼動環境でストアをテストすることは、Adobe Commerceの公式の推奨事項です。

## 解決策：実稼動サブドメインの使用

現在のライブサイトをベースドメイン（`prod.example.com`）に維持したまま、実稼動環境のクラウドインフラストラクチャストアに新しいAdobe Commerceを格納するには、第 1 レベルのサブドメイン（`example.com`）を使用します。

Adobe Commerce on cloud infrastructure プロジェクトを計画する際には、そのような実稼動サブドメインを指定し、クラウドインフラストラクチャチームに対して、サブドメインを Fastly サービスに指定するようにリクエストできます。

クラウドインフラストラクチャプロジェクトでAdobe Commerce内のサブドメインを処理するには、次の手順に従います。

* [ サポートチケットを送信 ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) サブドメインを Fastly サービス/Nginx 設定に追加することをリクエスト（cloud infrastructure Pro プランアーキテクチャ上のAdobe Commerceの場合）。
* 対応する DNS 設定を自分で設定します。

サブドメインの設定手順を実行した後で、次の手順を実行して実稼動ドメインの SSL 証明書を検証する必要があります。

* 実稼動ドメインの SSL 検証用の DNS TXT レコードをアップロードします。
* [ サポートチケットを送信 ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)SSL 証明書の実稼動ドメインの検証をリクエストします。

サブドメインを使用すると、今後ストアの「ソフト起動」を実行できます。これは、対応する DNS 設定の更新のみが必要なためです。

## 関連ドキュメント

サポートナレッジベースでは、

* [ ステージング環境と実稼動環境での Fastly DNS 設定 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/configure-fastly-dns-settings-on-staging-and-production-environments.html)
* [ クラウド上のスタータープラン用に Fastly を設定する ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/set-up-fastly-for-starter-plan-on-cloud.html)
* [ クラウドインフラストラクチャー上でのAdobe Commerceの立ち上げに対する潜在的なブロッカー ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/blockers-launching-on-magento-commerce-cloud.html)

開発者向けドキュメントでは、

* [Fastly の概要 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/fastly.html)
* [ 運用開始チェックリスト：Fastly の DNS 設定 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/checklist.html)
