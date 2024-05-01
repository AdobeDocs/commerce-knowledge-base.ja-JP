---
title: Adobe CommerceのNew Relicを使用したパフォーマンスのトラブルシューティング
description: この記事では、New Relicを使用して、クラウドインフラストラクチャー上でAdobe Commerceのパフォーマンスの問題を解決するためのトラブルシューティング手順を説明します。 また、詳しい情報を得るためのリソースも提供します。 問題のリストを以下に示します。 サポートナレッジベースでトラブルシューティング手順を確認するには、をクリックしてください。'
exl-id: 0a22beb7-18b0-47eb-a6b8-63b7322b392c
feature: Observability
role: Developer
source-git-commit: 324cce66df1e4ab7ec4ef8fb6512c3acbabdf3ab
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---

# Adobe CommerceのNew Relicを使用したパフォーマンスのトラブルシューティング

この記事では、New Relicを使用して、クラウドインフラストラクチャー上でAdobe Commerceのパフォーマンスに関する問題を解決するためのトラブルシューティング手順を説明します。 また、詳しい情報を得るためのリソースも提供します。 次の表で取り上げる問題と、推奨されるリソースは次のとおりです。

* Apdex スコアの低さ
* 高い CPU 使用率
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
<p>New Relic <a href="https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measuring-user-satisfaction">Apdex スコア</a> web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。</p>
</td>
<td>
<p>にログインしました <a href="https://login.newrelic.com/login">New Relic</a> / APM /概要 概要ページの右側に、Apdex スコア グラフが表示されます。 Apdex スコアが 0.5 以下の場合は、注意が必要であり、調査が必要であることを保証します。web トランザクションの時間（サーバーリクエスト）:</p>
<ol>
<ol>
<li>へのログイン <a href="https://login.newrelic.com/login">New Relic</a> / APM / （アプリを選択）/概要 メインのグラフドロップダウンフィルターで、フィルターが web トランザクション時間に設定されていることを確認します。 「トランザクション」テーブルの下で、アプリサーバー時間を探します。 長時間実行されているトランザクションや疑わしいトランザクションがあるかどうかを確認します。</li>
<li>監視/ トランザクションに移動して個別に調査し、web および最も時間のかかるフィルターを必ず設定してください<em>.</em>
</li>
<li>次に、リソースを消費するサードパーティモジュール（支払いプロバイダー、ERP など）を検索します。</li>
<li>APM の「監視」セクションで、<ol>
<li>「取引」をクリックします。</li>
<li>下にスクロールし、「すべてのトランザクションテーブルを表示」をクリックします。</li>
<li>トランザクションは、次の基準で並べ替えることができます <a href="https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems#table_view">各種パラメーター</a> 疑いを引き起こすものにジャンプします。</li>
<li>Apdex スコアが低い、カウントが異常に多い、平均時間が長い、またはディスサット % が高いトランザクションを確認します。</li>
<li>個々のトランザクションをクリックします。 問題を解決できない場合は、 <a href="/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket">サポートチケットを送信します。</a>
</li>
<li>さらに調査する必要がある場合は、web 以外のトランザクションの確認を検討します。</li>
</ol>
</li>
</ol>
</ol>
<p>非 Web トランザクション時間（操作およびバックグラウンド・タスク）:</p>
<ol>
<ol>
<li>へのログイン <a href="https://login.newrelic.com/login">New Relic</a> / APM / （アプリを選択）/概要 メイングラフドロップダウンフィルターで非 web トランザクション時間を必ず選択してください。 「トランザクション」 テーブルで個々のトランザクションをクリックします。 長時間実行されているトランザクションや疑わしいトランザクションを探します。 これには、バックエンドジョブ、cron ジョブ、または読み込み/書き出しジョブ（サードパーティを含む）が含まれます。</li>
</ol>
</ol>
</td>
<td>
<p>New Relic Apdex スコアについて詳しくは、以下を参照してください。 <a href="https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction">New Relic ドキュメント &gt; APM Apdex &gt; ユーザー満足度の測定</a>. 以下も参照してください。 <a href="/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce-apdex-warning-alert.md">Adobe Commerceの管理アラート：Apdex 警告アラート</a> サポートナレッジベースで。</p>
</td>
</tr>
<tr>
<td>
<p>高い CPU 使用率：</p>
<p>CPU 使用率が高い場合は、MySQL、Redis など、特にビジー状態のサービスがあることを示しています。</p>
</td>
<td>
<ol>
<li>へのログイン <a href="https://login.newrelic.com/login">New Relic</a> / インフラストラクチャ / プロセス。</li>
<li>CPU グラフを確認して、CPU 時間を 100% 以上使用しているスタックプロセスや高消費プロセスがあるかどうかを確認し、インスタンスのプロセッサー数と比較します。 リソース使用率のピークに注意を払う 停止した cron でない限り、プロセスを強制終了することはお勧めしません。</li>
</ol>
</td>
<td>
<p>パフォーマンス指標、特に個々のプロセスまたはプロセスのグループの CPU の割合、I/O バイトおよびメモリ使用量の詳細については、を参照してください。 <a href="https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes">New Relic ドキュメント/インフラストラクチャ UI ページ/インフラストラクチャホストページ/プロセス タブ</a>.</p>
</td>
</tr>
<tr>
<td>
<p>高い I/O 操作：顧客ごとに個別に割り当てますが、平均とは大きく異なります。</p>
</td>
<td>
<p>以前の平均 I/O 操作と比較して、異常なスパイクを探します。</p>
<ol>
<li>へのログイン <a href="https://login.newrelic.com/login">New Relic</a> / インフラストラクチャ / プロセス。</li>
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
<li>へのログイン <a href="https://login.newrelic.com/login">New Relic</a> / APM /概要 ドロップダウングラフフィルターで、フィルターが「Web トランザクション時間」に設定されていることを確認します。</li>
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

注意： <code>更新</code> または <code>挿入</code>クエリは、最も CPU を消費するクエリです。</li>
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
<p>特定のパフォーマンスの問題の調査について詳しくは、次を参照してください。 <a href="https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems#tx_functions">New Relic ドキュメント / APM UI ページ / トランザクションページ / ドリルダウン関数の使用</a>.</p>
</td>
</tr>
</tbody>
</table>
