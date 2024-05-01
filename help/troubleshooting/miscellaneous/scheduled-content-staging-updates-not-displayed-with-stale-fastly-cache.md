---
title: スケジュールされたコンテンツステージングの更新が、古い Fastly キャッシュで表示されない
description: この記事では、コンテンツのステージングと Fastly を使用する際に、Adobe Commerce ストアにスケジュールされた更新が表示されない問題を修正します。 この問題は、デフォルトで Fastly ソフトパージが有効になっていることが原因です。 この機能により、アプリケーションのリソースの負荷が軽減され、2 回目のリクエストで新しいキャッシュのみが再生成されます。 これを解決するには、Commerce Admin で CMS ページをパージを有効にして、常に新規コンテンツを再生成および提供します。
exl-id: becbffaa-b6dd-4e9b-894e-17901c40223a
feature: CMS, Cache, Page Content, Staging
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# スケジュールされたコンテンツステージングの更新が、古い Fastly キャッシュで表示されない

この記事では、コンテンツのステージングと Fastly を使用する際に、Adobe Commerce ストアにスケジュールされた更新が表示されない問題を修正します。 この問題は、デフォルトで Fastly ソフトパージが有効になっていることが原因です。 この機能により、アプリケーションのリソースの負荷が軽減され、2 回目のリクエストで新しいキャッシュのみが再生成されます。 これを解決するには、Commerce Admin で CMS ページをパージを有効にして、常に新規コンテンツを再生成および提供します。

## 問題

ストアのコンテンツアセット（ページ、製品、ブロックなど）のスケジュールされた更新 更新開始直後はストアフロントに表示されません。 この問題は、 [コンテンツのステージング](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging.html) 機能。

## 原因：

Fastly のソフトパージ機能（デフォルトで有効）により、Adobe Commerce ストアフロントは送信時に古い（古い）キャッシュされたコンテンツを引き続き受け取ります **第 1** 更新されたアセットの Fastly へのリクエスト。 Fastly では、サイトデータを再生成するための 2 つ目のリクエストが必要です。

その結果、更新されたコンテンツに対する 2 回目のリクエストが行われるまで、Fastly は古いコンテンツを提供する場合があります。

**予想されるキャッシュ：** コンテンツステージングを使用してコンテンツアセットの更新をスケジュールすると、Adobe Commerceから Fastly にキャッシュを更新するリクエストが送信されます。 Fastly は、以前にキャッシュされたコンテンツを（コンテンツを削除せずに）無効にし、更新されたコンテンツの提供を開始します。

**実際のキャッシュ：** 受信時に Fastly が古いコンテンツを引き続き提供する場合 **第 1** 更新されたコンテンツのリクエストの場合、再生済みの正しいコンテンツが受信された後にのみ送信されます **第 2** リクエスト。 この動作は、Web サイト全体のキャッシュを再生成せずに、トラフィックが証明済みの領域でのみキャッシュを更新することで、サーバーの負荷を軽減するために実装されました。 Fastly は、キャッシュを徐々に更新して、アプリケーションリソースを節約します。

## 解決策

最初のリクエストでも古いコンテンツを提供することが許容できない場合は、ソフトパージを無効にして、CMS ページをパージを有効にできます。

1. 管理者として、ローカルのCommerce管理者にログインします。
1. に移動 **ストア** > **設定** > **詳細** > **システム** > **フルページキャッシュ**.
1. を展開 **Fastly 設定**&#x200B;を展開します **詳細**.
1. を設定 **ソフトパージを使用** 対象： *不可*.
1. を設定 **CMS ページをパージ** 対象： *はい*.
1. クリック **設定を保存** ページの上部


![purge_options.png](assets/purge_options.png)

## 関連ドキュメント

* [パージオプションを設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html) （Commerce on Cloud Infrastructure ガイド）を参照してください。
* [コンテンツのステージング](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging.html) （コンテンツとデザインのドキュメント）
* [古いコンテンツの提供](https://docs.fastly.com/guides/performance-tuning/serving-stale-content) （Fastly のドキュメント）。
