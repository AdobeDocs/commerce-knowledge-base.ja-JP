---
title: スループットの高いAJAX リクエストが原因で、パフォーマンスが低下する
description: この記事では、一部の高スループットリクエストがサーバー負荷とトラフィックの増加を引き起こすことで発生する、Adobe Commerce オンプレミスまたはAdobe Commerce on cloud infrastructure サイトのパフォーマンスの問題に対するソリューションを説明します。
exl-id: 68dfca8a-826c-4476-acaf-a139052b5dcc
feature: Cache
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# スループットの高いAJAX リクエストが原因で、パフォーマンスが低下する

この記事では、一部の高スループットリクエストがサーバー負荷とトラフィックの増加を引き起こすことで発生する、Adobe Commerce オンプレミスまたはAdobe Commerce on cloud infrastructure サイトのパフォーマンスの問題に対するソリューションを説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x
* Adobe Commerce オンプレミス 2.2.x、2.3.x

>[!NOTE]
>
>この問題は、クラウドインフラストラクチャー上のAdobe Commerceとオンプレミス上のAdobe Commerceの両方のバージョン 2.3.4 で修正されました。

### 問題

重要なAJAX リクエストなどの高スループットリクエストが原因で、サイトのパフォーマンスが低下します。

### 原因：

高スループットのAJAX リクエストには、顧客のプライベートコンテンツに関連するリクエストが含まれます。

### 解決策

次の 3 つの解決策があります。

* [バージョン 2.3.4 へのアップグレード](https://devdocs.magento.com/cloud/project/project-upgrade.html). これが現在不可能な場合、 [問題を修正するパッチをインストールします](/help/troubleshooting/known-issues-patches-attached/performance-issues-caused-by-excessive-ajax-requests.md).
* 軽いリクエスト（キャッシュリクエストまたは顧客のプライベートコンテンツへの移動）を確保します。
* リクエストの数を減らします。

<u>リクエストの軽減（リクエストのキャッシュまたは顧客のプライベートコンテンツへの移動）</u>

各ページでトリガーされるサードパーティのAJAX リクエストがある場合は、これらのリクエストをキャッシュするか、顧客のプライベートコンテンツに移動しようとします。 これを行うには、マーチャントがGET HTTP メソッドを使用してカスタム AJAX リクエストを呼び出すようにします。 これにより、これらのリクエストが Fastly でキャッシュできるようになります。 キャッシュしてはいけないカスタム AJAX リクエストがある場合は、プライベートコンテンツ機能に従ってリファクタリングする必要があります。 手順については、を参照してください。 [非公開コンテンツ](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/cache/page-caching/private-content.html) 開発者向けドキュメントを参照してください。

<u>リクエストの数を減らす</u>

* 永続的な買い物かごを無効にすると、の数が増える可能性があります。 `customer/section/load` リクエスト。 の手順に従います [永続的な買い物かごパス](https://devdocs.magento.com/guides/v2.3/config-guide/prod/config-reference-most.html#persistent-shopping-cart-paths) アドビの開発者向けドキュメントで、永続的な買い物かごが有効になっているかどうかを確認します。
* でコンテンツの再読み込みまたは無効化が必要な場合 `sections.xml` の手順に従います [プライベートコンテンツ：プライベートコンテンツを無効にします](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/cache/page-caching/private-content.html#invalidate-private-content) 開発者向けドキュメントを参照してください。 を使用していないことを確認してください `customerData.reload()` メソッドをカスタマイズ内で直接実行します。
* 同じページ上の他のPOST AJAX リクエストを確認します。 Google Chrome ブラウザーで、Google Chrome デベロッパーツールを開きます。 「」をクリック **ネットワーク** tab キーを押してから、 **XHR** タブをクリックすると、特定のページからのすべてのAJAX リクエストのリストが表示されます。 次に、各リクエストをクリックし、フィールドでリクエストメソッドをGETリクエストにする必要があります。 メモ：Google Chrome は例として使用され、他のブラウザーでも同様に実行できます。
* Google Tag Manager （GTM）機能を確認します。これは特定のAJAX リクエストです。 ユーザーはこのAJAXを削除し、プライベート機能を使用してカスタマイズをリファクタリングして、サーバーへのリクエストの合計数を減らすことができます。
* Adobe Commerceのバナーが有効になっているが、使用されていないことを確認します。 次が必要になる場合があります [サイトのパフォーマンスを向上させるために、Adobe Commerce バナーの出力を無効にします](/help/troubleshooting/miscellaneous/disable-magento-banner-output-to-improve-site-performance.md).

### 関連資料

個人顧客コンテンツの詳細については、を参照してください。 [非公開コンテンツ](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/cache/page-caching/private-content.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=ajax%20requests) 開発者向けドキュメントを参照してください。
