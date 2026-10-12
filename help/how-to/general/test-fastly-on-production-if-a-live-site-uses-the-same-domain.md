---
title: ライブサイトで同じドメインを使用する場合は、実稼動環境でFastlyをテストします
description: 実稼動ドメイン（「example.com」）でライブサイトを稼働しており、Fastly CDNが有効になっているクラウドインフラストラクチャの実稼動環境でAdobe Commerce上の新しいストアをテストする必要がある場合は、以前にFastlyに追加したサブドメイン（「prod.example.com」など）を使用して、ローンチ前のテストアクティビティを行うことをお勧めします。 この記事では、詳細について説明し、関連するAdobe Commerceのドキュメントリソースへの便利なリンクを提供します。
exl-id: bc9d11c8-ce47-461d-b5b8-c03494bc4ceb
feature: Cache
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%
---
# ライブサイトで同じドメインを使用する場合は、実稼動環境でFastlyをテストします

実稼動ドメイン （`example.com`）でライブサイトを稼働中で、Fastly CDNが有効になっているクラウドインフラストラクチャの実稼動環境でAdobe Commerce上の新しいストアをテストする必要がある場合は、起動前のテストアクティビティのために、以前にFastlyに追加したサブドメイン （`prod.example.com`など）を使用することをお勧めします。 この記事では、詳細について説明し、関連するAdobe Commerceのドキュメントリソースへの便利なリンクを提供します。

## イシュー

`example.com`実稼動ドメインを使用する現在のストアはライブで動作しています。 ただし、新しいストアをテストする必要があります。これは、Adobe Commerceクラウドインフラストラクチャで構築され、Fastly フルページキャッシュサービスが有効になっている状態で、実稼動環境にデプロイされます。

問題は、Adobe Commerce on cloud infrastructure プロジェクトの実稼動環境で同じライブドメイン （`example.com`）が使用されており、同じドメインで現在のライブストアを同時に実行して、新しいサイトをこのドメインに切り替えることができないことです。

### 本番環境でのテストにFastlyを使用する理由？

理論的には、Fastly CDNを使用せずにスキップし、フルページキャッシュを有効にせずに、実稼動環境のクラウドインフラストラクチャストアでAdobe Commerceをテストできます。

ただし、フルページキャッシュを有効にすると、ストアのパフォーマンスが異なります。CDNでテストしていないサイトの実際のライブパフォーマンスを起動前に把握することはできません。 Fastly CDNを有効にして実稼動環境でストアをテストすることは、Adobe Commerceの公式の推奨事項です。

## 解決策：実稼動サブドメインの使用

実稼動環境の新しいAdobe Commerce on cloud infrastructure ストアに対して、現在のライブサイトをベースドメイン （`example.com`）に維持しながら、1番目のサブドメイン （`prod.example.com`）を使用します。

Adobe Commerce on cloud infrastructure プロジェクトを計画する際には、このような実稼動サブドメインを指定し、クラウドインフラストラクチャチームに対して、そのサブドメインをFastly サービスに誘導するようにリクエストできます。

Adobe Commerce on cloud infrastructure プロジェクト内でサブドメインを処理するには、次の手順に従います。

* [&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を送信して、サブドメインをFastly サービス/Nginx設定に追加することをリクエストします（Adobe Commerce on cloud infrastructure Pro プランアーキテクチャの場合）。
* 対応するDNS設定を自分の側で設定します。

サブドメイン設定の手順を実行した後、次の手順を実行して、SSL証明書の実稼動ドメインを検証する必要があります。

* 実稼動ドメインのSSL検証用にDNS TXT レコードをアップロードします。
* SSL証明書の実稼動ドメインの検証を要求する[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を送信します。

サブドメインを使用すると、将来ストアの「ソフトローンチ」を実行できます。このようなローンチでは、対応するDNS設定を更新する必要があるだけです。

## 関連ドキュメント

サポートナレッジベース：

* [ステージング環境と実稼動環境でのFastly DNS設定](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/configure-fastly-dns-settings-on-staging-and-production-environments.html?lang=ja)
* [Adobe Commerce on cloud infrastructureの導入を阻む潜在的な障壁](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/blockers-launching-on-magento-commerce-cloud.html?lang=ja)

アドビの開発者ドキュメントには、次のようなものがあります。

* [Fastlyの概要](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/fastly.html?lang=ja)
* [ライブチェックリスト：FastlyのDNS設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/checklist.html?lang=ja)
