---
title: クラウドインフラストラクチャー上で一時的なAdobe Commerceのアップサイズをリクエストする方法
description: 高トラフィックが予想されるオンラインイベントを計画している場合、またはサイトが突然高トラフィックのイベントに遭遇した場合は、[ サポートチケット ] （/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket）を申請して、クラウドインフラストラクチャストア上のAdobe Commerceの一時的なクラウドキャパシティを増やすようにリクエストできます。
exl-id: 561e2bdd-718a-45c1-8b6c-a0e3a6c8ad04
feature: Cloud, Iaas
source-git-commit: a445bae7f013b29cb83fc96eb26dcbfd186a4de7
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---

# クラウドインフラストラクチャー上で一時的なAdobe Commerceのアップサイズをリクエストする方法

組織が高トラフィックを期待するオンラインイベントを計画している場合や、サイトが突然高トラフィックのイベントに遭遇した場合は、 [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) Adobe Commerce on cloud infrastructure store の一時的なクラウド容量の追加をリクエストするには、次の手順を実行します。

>[!NOTE]
>
>緊急時以外のアップサイズリクエストの場合は、48 営業時間通知が必要です。 プロモーションキャンペーンのアップサイズは、サイトが完全に機能しない場合や、予想よりもはるかに高いトラフィックを受信し、パフォーマンスが大幅に低下している場合を除き、緊急とは見なされません。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [サポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf).

## 高トラフィックイベントの識別方法

New Relic アラートでは、ベースラインアラート条件を使用して、データの動作に合わせるしきい値を定義できます。

ベースラインアラートは、次のようなアラート条件を作成する場合に役立ちます。

* データの動作が異常な場合にのみ通知します。
* 日次または週次のトレンドを含む、変化するデータやトレンドに動的に適応する。

さらに、ベースラインアラートは、動作が不明な新しいアプリケーションでもうまく機能します。

New Relicについて詳しくは、こちらのリンクを参照してください [Intelligence を適用した異常値検出](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/anomaly-detection/anomaly-detection-applied-intelligence/).

高いトラフィックイベントを示唆するアラート通知が届いた場合は、考慮が必要な場合があります [サポートチケットの送信](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket) 追加容量を要求しています。 次の手順に従います。

## サイトのパフォーマンスの監視方法

Adobeは、クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャとクラウドインフラストラクチャー上のAdobe Commerce Starter プランアーキテクチャ実稼動環境では、次の主要業績評価指標を追跡するための一連のNew Relic アラートポリシーを提供します。

* [Apdex スコア](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction)
* エラー率
* ディスク容量（Pro アーキテクチャの実稼動環境でのみ使用可能）

これらのポリシーは、業界のベスト・プラクティスに基づいて、パフォーマンスに影響を及ぼす警告や重要な条件に対するしきい値を設定します。 アラートしきい値をトリガーにするインフラストラクチャまたはアプリケーションの問題がサイトで発生すると、New Relicからアラート通知が送信されるので、問題にプロアクティブに対処できます。 これらのポリシーを使用するには、アラートメッセージを受信する通知チャネルを設定する必要があります。

次の方法については、このリンクを参照してください [パフォーマンスベースのアラートの設定](/docs/commerce-cloud-service/user-guide/monitor/new-relic.html#monitor-performance-with-managed-alerts).

## 一時的なアップサイズをリクエストする手順

以下の手順に従って、 [サポートチケット](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket) 一時的な追加クラウド容量をリクエストするには：

を送信 [Adobe Commerce サポートセンターのサポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)：次の情報を入力します。

>[!NOTE]
>
>この *休日サージ要求* 選択は、10 月から 12 月の間のオプションです。

1. サポートを受けようとするAdobe Commerce製品を選択してください。
1. 最初の 4 つのフィールド（製品、組織、実装タイプ、件名）に入力します。
1. を選択 *Adobe Commerce クラウドインフラストラクチャ* が含まれる **連絡先の理由** ドロップダウン。
1. を選択 *休日のサージ容量リクエスト* が含まれる **Adobe Commerce インフラストラクチャ連絡先の理由** ドロップダウンオプション。 クリック **OK** 一時的な追加クラウド容量リクエストに対する 48 営業時間前の通知をリクエストするポップアップメッセージ
1. 必須フィールドの日付を選択 **開始日のサイズ変更** および **終了日のサイズ変更**. 推奨 **開始時間のサイズ変更** また、は必須フィールドです。
1. 次の 4 つのフィールドに入力します。
1. が含まれる **説明** フィールドに、サイズに関する追加情報がある場合は、ここに入力します。 特に大きなサイズが要求されない場合は、次に大きい環境サイズの容量までアップサイズされます。 サージリクエストは、デフォルトで現在のサイズより次に大きいサイズに設定されます。 追加容量が必要な場合は、そのを **説明** フィールド。 容量の増加は、契約されたサージ日数または vCPU 日数から差し引かれます。 通常の容量増加期間は 5 日ですが、必要な日数が増減する場合は、で指定してください [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

>[!NOTE]
>
>アップサイズがスケジュールされると、自動システムによってクラウドインスタンスのサイズが調整されます。 手順が完了すると、チケット通知が届かないことがあります。 Adobe Commerceの監視ツールを使用すると、AWSまたは Azure インスタンスタイプをに表示できます [変更の確認](/help/how-to/general/check-vcpu-using-observation-for-adobe-commerce.md).

## アップサイズの履歴の表示

リクエストされたサイズ変更の履歴は、で確認できます [プロジェクトポータル（オンボーディング UI）](/docs/commerce-cloud-service/start/onboarding.html#cloud-project-portal-(onboarding-ui))、の下 **プロジェクト** > **サービス** > **CPU 使用率のトラッキング**.
サイズ変更リクエストごとに、次の情報を使用できます。

* **サイズの開始日**：アップサイズリクエストの日付。
* **サイズ終了日**：クラスターが以前のサイズに戻された日付。
* **vCPU サイズ**：アップサイズ後のクラスターのサイズ。
* **使用日数**：クラスターがアップサイズされたままであった日数。
* **期間 vCPU**:vCPU サイズが使用日数によって変更されました。 （例えば、vCPU サイズ 192 x 25 日は 4,800 です）。


## 関連資料

* サイトのパフォーマンスを測定および改善する方法に関するインサイト、方法、例については、サポートナレッジベースの次の詳細な記事を参照してください。
   * [クラウド上のAdobe Commerceの CPU 割り当ての計算](/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-cpu-allocation-calculation.html)
   * [クラウド上のAdobe Commerceでホストのインスタンスのアップサイズが必要かどうかを確認する](/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-if-upsize-for-hosts-instances-is-needed.html)
   * [クラウド上のAdobe Commerceに対するホストの CPU 設定の確認](/docs/commerce-knowledge-base/kb/how-to/magento-commerce-cloud-check-hosts-cpu-configuration.html)
* 停止を特定する方法については、次を参照してください。 [クラウド上のAdobe Commerceの停止の特定と測定](/docs/commerce-knowledge-base/kb/how-to/how-to-identify-outages.html) サポートナレッジベースで。
* 容量の増加を利用する必要をなくすためにサイトのパフォーマンスを向上させる方法については、開発者向けドキュメントで次の記事を参照してください。
   * [画像サイズ](/docs/commerce-admin/catalog/products/digital-assets/product-image-config.html#product-image-resizing)
   * [完全なページキャッシュ](/docs/commerce-admin/systems/tools/cache-management.html#full-page-caching)
   * [ECE-Tools](/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/package-overview.html)
