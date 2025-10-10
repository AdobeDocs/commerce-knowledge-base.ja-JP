---
title: クラウドインフラストラクチャー上で一時的なAdobe Commerceのアップサイズをリクエストする方法
description: 高トラフィックが予想されるオンラインイベントを計画している場合、またはサイトが突然高トラフィックのイベントに遭遇した場合は、[ サポートチケット ] （/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket）を申請して、クラウドインフラストラクチャストア上のAdobe Commerceの一時的なクラウドキャパシティを増やすようにリクエストできます。
exl-id: 561e2bdd-718a-45c1-8b6c-a0e3a6c8ad04
feature: Cloud, Iaas
source-git-commit: e59335b67e1f33e138e34cab93ce593836d14b48
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# クラウドインフラストラクチャー上で一時的なAdobe Commerceのアップサイズをリクエストする方法

高トラフィックが予想されるオンラインイベントを計画している場合、またはサイトが突然、高トラフィックイベントに遭遇した場合は、[&#x200B; サポートチケット &#x200B;](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) を申請して、Adobe Commerce on cloud infrastructure store の一時的なクラウド容量の追加をリクエストできます。

>[!NOTE]
>
>緊急時以外のアップサイズリクエストの場合は、48 営業時間通知が必要です。 プロモーションキャンペーンのアップサイズは、サイトが完全に機能しない場合や、予想よりもはるかに高いトラフィックを受信し、パフォーマンスが大幅に低下している場合を除き、緊急とは見なされません。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [&#x200B; サポート対象バージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)。

## 高トラフィックイベントの識別方法

New Relic アラートでは、ベースラインアラート条件を使用して、データの動作に合わせるしきい値を定義できます。

ベースラインアラートは、次のようなアラート条件を作成する場合に役立ちます。

* データの動作が異常な場合にのみ通知します。
* 日次または週次のトレンドを含む、変化するデータやトレンドに動的に適応する。

さらに、ベースラインアラートは、動作が不明な新しいアプリケーションでもうまく機能します。

このリンクでは、New Relic[Applied Intelligence を使用した異常値検出 &#x200B;](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/anomaly-detection/anomaly-detection-applied-intelligence/) の詳細を説明します。

高トラフィックイベントを示唆するアラート通知が届いた場合は、追加容量のリクエスト [&#x200B; サポートチケットの送信 &#x200B;](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket) を検討する必要がある場合があります。 次の手順に従います。

## サイトのパフォーマンスの監視方法

Adobeは、クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャとクラウドインフラストラクチャー上のAdobe Commerce Starter プランアーキテクチャ実稼動環境では、次の主要業績評価指標を追跡するための一連のNew Relic アラートポリシーを提供します。

* [Apdex スコア &#x200B;](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction)
* エラー率
* ディスク容量（Pro アーキテクチャの実稼動環境でのみ使用可能）

これらのポリシーは、業界のベスト・プラクティスに基づいて、パフォーマンスに影響を及ぼす警告や重要な条件に対するしきい値を設定します。 アラートしきい値をトリガーにするインフラストラクチャまたはアプリケーションの問題がサイトで発生すると、New Relicからアラート通知が送信されるので、問題にプロアクティブに対処できます。 これらのポリシーを使用するには、アラートメッセージを受信する通知チャネルを設定する必要があります。

このリンクでは、[&#x200B; パフォーマンスベースのアラートの設定 &#x200B;](/docs/commerce-cloud-service/user-guide/monitor/new-relic.html#monitor-performance-with-managed-alerts) 方法を説明します。

## 一時的なアップサイズをリクエストする手順

一時的なクラウド容量の追加をリクエストするには、次の情報を記載した [&#x200B; サポートチケット &#x200B;](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) をAdobe Commerce サポートセンターで送信します。

>[!NOTE]
>
>*ホリデーサージリクエスト* の選択は、10 月から 12 月の間のオプションです。

1. サポートが必要な [!DNL Adobe Commerce] 製品を選択します。
   * [!DNL Commerce Cloud]
   * [!DNL Commerce on Managed Service]

1. 次のフィールドに入力します。
   * **[!UICONTROL Case Title]**
   * **[!UICONTROL Case Description]** *（イシューとコンテキストを明確に説明していることを確認してください）*

1. *ドロップダウンメニューから* インフラストラクチャ変更リクエスト **[!UICONTROL Issue Reason]** を選択します。

1. ドロップダウンメニューから **[!UICONTROL Environment]** を選択します。

1. ドロップダウンメニューから適切な **[!UICONTROL Product Version]** を選択します。

1. *ドロップダウンメニューから* クラウドプロジェクトのサイズ変更（vCPU） **[!UICONTROL Which Infra Change you would like to do today]** を選択します。

1. **[!UICONTROL Architecture]** を選択します。
   * *デフォルトのアーキテクチャ：* *サイズを選択* ドロップダウンメニューから **次に使用可能なサイズ** を選択します。
   * *スケールされたアーキテクチャ：* 選択すると、画面が変更されて、次の 2 つの追加フィールドが表示されます。
      * *Web ノードのサイズ*
      * *サービスノードのサイズ**（各ノードに必要なサイズを入力します）*

1. **[!UICONTROL From Date]** を UTC 形式（日付と時刻）で入力します。

1. **[!UICONTROL To Date]** を UTC 形式（日付と時刻）で入力します。

1. **[!UICONTROL Project URL]***指定します（https://accounts.magento.cloud/にあり、通常は `https://[REGION].magento.cloud/projects/PROJECT_ID` の形式です）*

1. **[!UICONTROL Project ID]** を入力します。

1. **[!UICONTROL Affected URL]***指定してください（`http://` または `https://` で始める必要があります）*

1. 「**[!UICONTROL Priority]**」を選択します。

1. 「**[!UICONTROL Business Impact]**」を選択します。

1. **[!UICONTROL Time Zone]** *（例：`(UTC-5:00) Indiana (East)`）* を確認します

1. **[!UICONTROL Phone Number]***を入力してください（例：`+12015550123`）*

1. 「**[!UICONTROL Submit]**」をクリックして、サポートケースを確定します。

>[!NOTE]
>
>アップサイズがスケジュールされると、自動システムによってクラウドインスタンスのサイズが調整されます。 手順が完了すると、チケット通知が届かないことがあります。 Adobe Commerceの監視ツールを使用して、AWSまたは Azure インスタンスタイプを表示し、[&#x200B; 変更を確認 &#x200B;](/help/how-to/general/check-vcpu-using-observation-for-adobe-commerce.md) ることができます。

## アップサイズの履歴の表示

**CSM （Customer Success Manager）** に情報を要求すると、要求されたサイズ変更の履歴を表示できます。
サイズ変更リクエストごとに、次の情報を使用できます。

* **サイズ開始日**：アップサイズリクエストの日付。
* **サイズ終了日**：クラスターが以前のサイズに戻された日付。
* **vCPU サイズ**：アップサイズ後のクラスターのサイズです。
* **使用日数**：クラスターがアップサイズのままであった日数。
* **期間 vCPU**:vCPU サイズが使用日数だけ変更されました。 （例えば、vCPU サイズ 192 x 25 日は 4,800 です）。


## 関連資料

* サイトのパフォーマンスを測定および改善する方法に関するインサイト、方法、例については、サポートナレッジベースの次の詳細な記事を参照してください。
   * [Adobe Commerce on cloud のCPU配分の計算](/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-cpu-allocation-calculation.html)
   * [クラウド上のAdobe Commerceでホストのインスタンスのアップサイズが必要かどうかを確認する](/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-if-upsize-for-hosts-instances-is-needed.html)
   * [クラウド上のAdobe Commerceに対するホストのCPU設定の確認](/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-hosts-cpu-configuration.html)
* 停止を特定する方法について詳しくは、サポートナレッジベースの [Adobe Commerce on cloud の停止の特定と測定 &#x200B;](/docs/commerce-knowledge-base/kb/how-to/how-to-identify-outages.html) を参照してください。
* 容量の増加を利用する必要をなくすためにサイトのパフォーマンスを向上させる方法については、開発者向けドキュメントで次の記事を参照してください。
   * [画像サイズ](/docs/commerce-admin/catalog/products/digital-assets/product-image-config.html#product-image-resizing)
   * [完全なページキャッシュ](/docs/commerce-admin/systems/tools/cache-management.html#full-page-caching)
   * [ECE-Tools](/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/package-overview.html)
