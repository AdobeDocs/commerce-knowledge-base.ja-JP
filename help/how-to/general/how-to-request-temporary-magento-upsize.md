---
title: クラウドインフラストラクチャー上で一時的なAdobe Commerceのアップサイズをリクエストする方法
description: 高トラフィックが予想されるオンラインイベントを計画している場合、またはサイトが突然高トラフィックのイベントに遭遇した場合は、[ サポートチケット ] （/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket）を申請して、クラウドインフラストラクチャストア上のAdobe Commerceの一時的なクラウドキャパシティを増やすようにリクエストできます。
exl-id: 561e2bdd-718a-45c1-8b6c-a0e3a6c8ad04
feature: Cloud, Iaas
source-git-commit: 357e0acb1c849079ff0fe9f53fe386f60475c7f9
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# クラウドインフラストラクチャー上で一時的なAdobe Commerceのアップサイズをリクエストする方法

高トラフィックが予想されるオンラインイベントを計画している場合、またはサイトが突然、高トラフィックイベントに遭遇した場合は、[ サポートチケット ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) を申請して、Adobe Commerce on cloud infrastructure store の一時的なクラウド容量の追加をリクエストできます。

>[!NOTE]
>
>緊急時以外のアップサイズリクエストの場合は、48 営業時間通知が必要です。 プロモーションキャンペーンのアップサイズは、サイトが完全に機能しない場合や、予想よりもはるかに高いトラフィックを受信し、パフォーマンスが大幅に低下している場合を除き、緊急とは見なされません。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [ サポート対象バージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)。

## 高トラフィックイベントの識別方法

New Relic アラートでは、ベースラインアラート条件を使用して、データの動作に合わせるしきい値を定義できます。

ベースラインアラートは、次のようなアラート条件を作成する場合に役立ちます。

* データの動作が異常な場合にのみ通知します。
* 日次または週次のトレンドを含む、変化するデータやトレンドに動的に適応する。

さらに、ベースラインアラートは、動作が不明な新しいアプリケーションでもうまく機能します。

このリンクでは、New Relic[Applied Intelligence を使用した異常値検出 ](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/anomaly-detection/anomaly-detection-applied-intelligence/) の詳細を説明します。

高トラフィックイベントを示唆するアラート通知が届いた場合は、追加容量のリクエスト [ サポートチケットの送信 ](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket) を検討する必要がある場合があります。 次の手順に従います。

## サイトのパフォーマンスの監視方法

Adobeは、クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャとクラウドインフラストラクチャー上のAdobe Commerce Starter プランアーキテクチャ実稼動環境では、次の主要業績評価指標を追跡するための一連のNew Relic アラートポリシーを提供します。

* [Apdex スコア ](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction)
* エラー率
* ディスク容量（Pro アーキテクチャの実稼動環境でのみ使用可能）

これらのポリシーは、業界のベスト・プラクティスに基づいて、パフォーマンスに影響を及ぼす警告や重要な条件に対するしきい値を設定します。 アラートしきい値をトリガーにするインフラストラクチャまたはアプリケーションの問題がサイトで発生すると、New Relicからアラート通知が送信されるので、問題にプロアクティブに対処できます。 これらのポリシーを使用するには、アラートメッセージを受信する通知チャネルを設定する必要があります。

このリンクでは、[ パフォーマンスベースのアラートの設定 ](/docs/commerce-cloud-service/user-guide/monitor/new-relic.html#monitor-performance-with-managed-alerts) 方法を説明します。

## 一時的なアップサイズをリクエストする手順

次の手順に従って、[ サポートチケット ](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket) を送信し、一時的なクラウド容量の追加をリクエストします。

次の情報を入力した後、[Adobe Commerce サポートセンターでのサポートチケット ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) を送信します。

>[!NOTE]
>
>*ホリデーサージリクエスト* の選択は、10 月から 12 月の間のオプションです。

1. サポートを受けようとするAdobe Commerce製品を選択してください。
1. 最初の 4 つのフィールド（製品、組織、実装タイプ、件名）に入力します。
1. **連絡先の理由 *ドロップダウンで「*Adobe Commerce クラウドインフラストラクチャ**」を選択します。
1. *2}Adobe Commerce インフラストラクチャの連絡先の理由* ドロップダウンオプションで、「{Holiday Surge Capacity Request **」を選択します。**&#x200B;一時的な追加のクラウド容量リクエストに対しては、48 営業時間前の通知をリクエストするポップアップメッセージで **OK** をクリックします。
1. 必須フィールド **開始日のサイズ変更** および **終了日のサイズ変更** の日付を選択します。 推奨される **開始時間のサイズ変更** も必須フィールドです。
1. 次の 4 つのフィールドに入力します。
1. サイズに関する追加情報がある場合は、「**説明**」フィールドに入力します。 特に大きなサイズが要求されない場合は、次に大きい環境サイズの容量までアップサイズされます。 サージリクエストは、デフォルトで現在のサイズより次に大きいサイズに設定されます。 追加容量が必要な場合は、「説明 **フィールドにそ** を入力してください。 容量の増加は、契約されたサージ日数または vCPU 日数から差し引かれます。 通常の容量増加期間は 5 日ですが、必要な日数が増減する場合は、[ サポートチケット ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) にその旨を記載してください。

>[!NOTE]
>
>アップサイズがスケジュールされると、自動システムによってクラウドインスタンスのサイズが調整されます。 手順が完了すると、チケット通知が届かないことがあります。 Adobe Commerceの監視ツールを使用して、AWSまたは Azure インスタンスタイプを表示し、[ 変更を確認 ](/help/how-to/general/check-vcpu-using-observation-for-adobe-commerce.md) ることができます。

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
   * [クラウド上のAdobe Commerceの CPU 割り当ての計算](/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-cpu-allocation-calculation.html)
   * [クラウド上のAdobe Commerceでホストのインスタンスのアップサイズが必要かどうかを確認する](/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-if-upsize-for-hosts-instances-is-needed.html)
   * [クラウド上のAdobe Commerceに対するホストの CPU 設定の確認](/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-hosts-cpu-configuration.html)
* 停止を特定する方法について詳しくは、サポートナレッジベースの [Adobe Commerce on cloud の停止の特定と測定 ](/docs/commerce-knowledge-base/kb/how-to/how-to-identify-outages.html) を参照してください。
* 容量の増加を利用する必要をなくすためにサイトのパフォーマンスを向上させる方法については、開発者向けドキュメントで次の記事を参照してください。
   * [画像サイズ](/docs/commerce-admin/catalog/products/digital-assets/product-image-config.html#product-image-resizing)
   * [完全なページキャッシュ](/docs/commerce-admin/systems/tools/cache-management.html#full-page-caching)
   * [ECE-Tools](/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/package-overview.html)
