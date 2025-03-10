---
title: Adobe CommerceのNew Relicを使用したパフォーマンスのトラブルシューティング
description: この記事では、New Relicを使用して、クラウドインフラストラクチャー上でAdobe Commerceのパフォーマンスに関する問題を解決するためのトラブルシューティング手順を説明します。 また、詳しい情報を得るためのリソースも提供します。 問題のリストを以下に示します。 サポートナレッジベースでトラブルシューティング手順を確認するには、をクリックしてください。
exl-id: 0a22beb7-18b0-47eb-a6b8-63b7322b392c
feature: Observability
role: Developer
source-git-commit: 27fed162416c619a08d757279a3405f1fa72e976
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Adobe CommerceのNew Relicを使用したパフォーマンスのトラブルシューティング

この記事では、New Relicを使用して、クラウドインフラストラクチャー上でAdobe Commerceのパフォーマンスに関する問題を解決するためのトラブルシューティング手順を説明します。 また、詳しい情報を得るためのリソースも提供します。 次の表で取り上げる問題と、推奨されるリソースは次のとおりです。

* Apdex スコアの低さ
* CPUの高い使用率
* 高い I/O オペレーション
* 機能停止

<table>
<tbody>
<tr>
<td>問題</td>
<td>トラブルシューティング</td>
<td>リソース</td>
</tr>
<tr>
<td>
<p>Apdex スコアの低さ：</p>
<p>New Relic<a href="https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measuring-user-satisfaction">Apdex スコア </a> は、web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。</p>
</td>
<td>
<p><a href="https://login.newrelic.com/login">New Relic</a>/APM/概要にログインします。 概要ページの右側に、Apdex スコア グラフが表示されます。 Apdex スコアが 0.5 以下の場合は、注意が必要であり、調査が必要であることを保証します。web トランザクションの時間（サーバーリクエスト）:</p>
<ol>
<ol>
<li><a href="https://login.newrelic.com/login">New Relic</a>/APM/（アプリを選択）/概要にログインします。 メインのグラフドロップダウンフィルターで、フィルターが web トランザクション時間に設定されていることを確認します。 「トランザクション」テーブルの下で、アプリサーバー時間を探します。 長時間実行されているトランザクションや疑わしいトランザクションがあるかどうかを確認します。</li>
<li>監視/ トランザクションに移動して個別に調査し、web および最も時間のかかる <em>.</em> のフィルターを設定します。
</li>
<li>次に、リソースを消費するサードパーティモジュール（支払いプロバイダー、ERP など）を検索します。</li>
<li>APM の「監視」セクションで、<ol>
<li>「取引」をクリックします。</li>
<li>下にスクロールし、「すべてのトランザクションテーブルを表示」をクリックします。</li>
<li>トランザクションを <a href="https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems#table_view"> 様々なパラメーター </a> で並べ替えて、疑わしいトランザクションにジャンプさせることができます。</li>
<li>Apdex スコアが低い、カウントが異常に多い、平均時間が長い、またはディスサット % が高いトランザクションを確認します。</li>
<li>個々のトランザクションをクリックします。 この問題が解決できない場合は、<a href="/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket"> サポートチケットを送信 </a> してください。
</li>
<li>さらに調査する必要がある場合は、web 以外のトランザクションの確認を検討します。</li>
</ol>
</li>
</ol>
</ol>
<p>非 Web トランザクション時間（操作およびバックグラウンド・タスク）:</p>
<ol>
<ol>
<li><a href="https://login.newrelic.com/login">New Relic</a>/APM/（アプリを選択）/概要にログインします。 メイングラフドロップダウンフィルターで非 web トランザクション時間を必ず選択してください。 「トランザクション」 テーブルで個々のトランザクションをクリックします。 長時間実行されているトランザクションや疑わしいトランザクションを探します。 これには、バックエンドジョブ、cron ジョブ、または読み込み/書き出しジョブ（サードパーティを含む）が含まれます。</li>
</ol>
</ol>
</td>
<td>
<p>New Relic Apdex スコアについて詳しくは、<a href="https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction">New Relic ドキュメント/APM Apdex/ユーザー満足度の測定 </a> を参照してください。 サポートナレッジベースの <a href="https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce-apdex-warning-alert">Managed alerts for Adobe Commerce: Apdex warning alert</a> も参照してください。</p>
</td>
</tr>
<tr>
<td>
<p>CPUの高い使用率：</p>
<p>CPUの使用率が高い場合は、MySQL、Redis など、特にビジー状態のサービスがあることを示している可能性があります。</p>
</td>
<td>
<ol>
<li><a href="https://login.newrelic.com/login">New Relic</a>/インフラストラクチャ/プロセスにログインします。</li>
<li>CPUのグラフを確認して、CPU時間を 100% 以上消費しているスタックプロセスや高い消費量のプロセスがあるかどうかを確認し、インスタンスのプロセッサー数と比較します。 リソース使用率のピークに注意を払う 停止した cron でない限り、プロセスを強制終了することはお勧めしません。</li>
</ol>
</td>
<td>
<p>パフォーマンス指標、特に個々またはプロセスグループのCPUのパーセンテージ、I/O バイトおよびメモリ使用量について詳しくは、<a href="https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes">New Relic ドキュメント/インフラストラクチャ UI ページ/インフラストラクチャホストページ/プロセス タブ </a> を参照してください。</p>
</td>
</tr>
<tr>
<td>
<p>高い I/O 操作：顧客ごとに個別に割り当てますが、平均とは大きく異なります。</p>
</td>
<td>
<p>以前の平均 I/O 操作と比較して、異常なスパイクを探します。</p>
<ol>
<li><a href="https://login.newrelic.com/login">New Relic</a>/インフラストラクチャ/プロセスにログインします。</li>
<li>1 秒あたりの I/O 読み取りバイト数のグラフを確認します。</li>
<li>スパイクの時間を記録します。</li>
<li>APM をクリックします。</li>
<li>メインのグラフ ドロップダウンフィルターで web トランザクション時間を必ず選択してください。</li>
<li>記録したスパイクの時間を設定します。</li>
<li>高い I/O 操作を引き起こしたトランザクションを検索します。</li>
<li>各トランザクショントレース/トレースの詳細にドリルダウンして、問題の原因を調べます。</li>
</ol>
</td>
</tr>
<tr>
<td>
<p>停止：New Relicが Apdex によって停止を特定します。 Apdex スコアグラフに赤い線が表示されます。これは、停止と見なされる Apdex &lt; 0.4 を示します。</p>
</td>
<td>
<p>障害の調査には、Web および Web 以外のトランザクション、データベース、サードパーティのトランザクションの調査など、いくつかの手順が必要になる場合があります。 Web トランザクション：</p>
<ol>
<li><a href="https://login.newrelic.com/login">New Relic</a>/APM/概要にログインします。 ドロップダウングラフフィルターで、フィルターが「Web トランザクション時間」に設定されていることを確認します。</li>
<li>時間枠を手動で絞り込みます。</li>
<li>「トランザクション」をクリックします。 フィルターが「Web」に設定され、「最も時間がかかっている」ことを確認します。 最も長く実行されているトランザクションを調査します。</li>
<li>さらに調査する必要がある場合は、web 以外のトランザクションの確認を検討します。</li>
</ol>
<p>Web 以外のトランザクション：</p>
<ol>
<li>概要ページに戻り、ドロップダウンフィルターの非 web トランザクションに切り替えます。</li>
<li>ページの一番下にあるトランザクショントレースを 1 つずつ確認します。</li>
<li>問題によっては、ボトルネックを見つけるために、PHP プロファイラのようなサードパーティツールを使用する必要があります。</li>
<li>さらに調査する必要がある場合は、データベースプロセスの調査を検討します。</li>
</ol>
<p>データベース プロセス：</p>
<ol>
<li>APM ページで、監視/ データベースに移動します。</li>
<li>最も時間がかかる順に並べ替えます。</li>
<li>上位のクエリを確認します。

メモ：<code>UPDATE</code> または <code> 挿入</code>クエリは、最もCPUを使用するクエリです。</li>
<li>並べ替え順セレクターからスループットに切り替え、データベースのスループットがドロップダウンに表示される原因となったプロセスを探します。</li>
<li>さらに調査する必要がある場合は、サードパーティのサービスの調査を検討してください。</li>
</ol>
<p>サードパーティのサービス：</p>
<ol>
<li>APM ページで、監視/外部サービスに移動します。</li>
<li>「並べ替え基準」ドロップダウンリストから最も遅い平均応答時間を選択します。</li>
<li>停止直前に発生したプロセスを探します。</li>
</ol>
</td>
<td>
<p>特定のパフォーマンスの問題の調査について詳しくは、<a href="https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems#tx_functions">New Relic ドキュメント/APM UI ページ/トランザクションページ/ドリルダウン関数の使用 </a> を参照してください。</p>
</td>
</tr>
</tbody>
</table>
