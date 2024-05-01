---
title: 実稼働サイトで同じドメインを使用している場合は、実稼動環境で Fastly をテストします
description: 実稼動ドメイン（「example.com」）で稼働中のサイトがあり、クラウドインフラストラクチャの実稼動環境で Fastly CDN を有効にしてAdobe Commerceで新しいストアをテストする必要がある場合は、ローンチ前のテストアクティビティには、以前に Fastly に追加したサブドメイン（「prod.example.com」など）を使用することをお勧めします。 この記事では、詳細を説明し、関連するAdobe Commerce ドキュメントリソースへの便利なリンクを提供します。
exl-id: bc9d11c8-ce47-461d-b5b8-c03494bc4ceb
feature: Cache
source-git-commit: 83b21845cd306336e1cb193a9541478c8a38eea8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 実稼働サイトで同じドメインを使用している場合は、実稼動環境で Fastly をテストします

実稼動ドメインで実稼働サイトがある場合（`example.com`）を選択し、Fastly CDN を有効にしてクラウドインフラストラクチャの実稼動環境でAdobe Commerce上の新しいストアをテストする必要があります。 `prod.example.com`（以前に Fastly に追加した）、ローンチ前のテストアクティビティ用。 この記事では、詳細を説明し、関連するAdobe Commerce ドキュメントリソースへの便利なリンクを提供します。

## 問題

を使用する現在のストア `example.com` 実稼動ドメインはライブで実行中です。 ただし、クラウドインフラストラクチャ上にAdobe Commerceを使用して構築し、Fastly フルページキャッシュサービスを有効にして実稼動環境にデプロイした、新しいストアをテストする必要があります。

問題は、Adobe Commerce on cloud infrastructure プロジェクトの実稼動環境で同じライブドメイン（`example.com`）を選択した場合は、新しいサイトをこのドメインに切り替えると同時に、現在のライブストアを同じドメインで実行することはできません。

### Fastly を実稼動環境でのテストに使用する理由

理論的には、Fastly CDN の使用をスキップし、フルページキャッシュを有効にせずに、実稼動環境のクラウドインフラストラクチャストアでAdobe Commerceをテストすることができます。

ただし、フルページキャッシュを有効にすると、ストアのパフォーマンスが異なります。起動前に CDN でテストしていない場合、サイトの実際のライブパフォーマンスがわかりません。 Fastly CDN を有効にした実稼動環境でストアをテストすることは、Adobe Commerceの公式の推奨事項です。

## 解決策：実稼動サブドメインの使用

第 1 レベルのサブドメイン（`prod.example.com`）を選択します（現在のライブサイトをベースドメインに維持したまま、実稼動環境のクラウドインフラストラクチャストアに新しいAdobe Commerceを格納する場合）（`example.com`）に設定します。

Adobe Commerce on cloud infrastructure プロジェクトを計画する際には、そのような実稼動サブドメインを指定し、クラウドインフラストラクチャチームに対して、サブドメインを Fastly サービスに指定するようにリクエストできます。

クラウドインフラストラクチャプロジェクトでAdobe Commerce内のサブドメインを処理するには、次の手順に従います。

* [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) fastly サービス/Nginx 設定にサブドメインを追加するリクエスト（クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャの場合）。
* 対応する DNS 設定を自分で設定します。

サブドメインの設定手順を実行した後で、次の手順を実行して実稼動ドメインの SSL 証明書を検証する必要があります。

* 実稼動ドメインの SSL 検証用の DNS TXT レコードをアップロードします。
* [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) ssl 証明書の実稼動ドメインの検証のリクエスト。

サブドメインを使用すると、今後ストアの「ソフト起動」を実行できます。これは、対応する DNS 設定の更新のみが必要なためです。

## 関連ドキュメント

サポートナレッジベースでは、

* [ステージング環境と実稼動環境での Fastly DNS 設定](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/configure-fastly-dns-settings-on-staging-and-production-environments.html)
* [クラウド上のスタータープラン用に Fastly を設定する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/set-up-fastly-for-starter-plan-on-cloud.html)
* [クラウドインフラストラクチャー上のAdobe Commerceでの起動に対する潜在的なブロッカー](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/blockers-launching-on-magento-commerce-cloud.html)

開発者向けドキュメントでは、

* [Fastly の概要](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/fastly.html)
* [運用開始チェックリスト：Fastly の DNS 設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/checklist.html)
