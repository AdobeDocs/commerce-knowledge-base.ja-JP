---
title: クラウドインフラストラクチャー上のAdobe CommerceのNew Relicのトラブルシューティング
description: この記事では、クラウドインフラストラクチャー上のAdobe CommerceのNew Relicをトラブルシューティングするためのリソースを提供します。
exl-id: ea763291-5c9b-4575-b2ee-820dbc367743
feature: Cloud, Observability, Paas
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe CommerceのNew Relicのトラブルシューティング

この記事では、クラウドインフラストラクチャー上のAdobe CommerceのNew Relicをトラブルシューティングするためのリソースを提供します。

<table>
<tbody>
<tr>
<td class="wysiwyg-text-align-center"><strong>問題</strong></td>
<td class="wysiwyg-text-align-center"><strong>原因：</strong></td>
<td class="wysiwyg-text-align-center"><strong>リソース</strong></td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" colspan="3">アクセスの問題</td>
</tr>
<tr>
<td>
<p><u>New Relicでプロジェクトを表示できません。</u></p>
<p>にログインしました <em>New Relic</em> ただし、表示/アクセス権が必要なプロジェクトが表示されません。</p>
</td>
<td>
<p>その場合は、管理者ユーザーがプロジェクトにユーザーを追加する必要があります。</p>
</td>
<td>
<p><a href="https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/faq/access-new-relic-services.html">New Relic サービスへのアクセス</a> サポートナレッジベースで。</p>
</td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" colspan="3">データの問題</td>
</tr>
<tr>
<td>
<p><u>インストール後のデータが欠落しています。</u></p>
<p>の使用 <a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/new-relic-diagnostics">New Relic診断ユーティリティ</a> 原因を特定しようとする。 それでも問題が解決しない場合は、エージェント固有のソリューションを検討してください。 これらのソリューションに関する記事へのリンクは、右側の列にあります。</p>
</td>
<td>
<p>データの欠落の原因は異なる可能性があります。 次が必要になる場合があります。</p>
<ul>
<li>エージェントがインストールされていることを確認します。</li>
<li>アプリ名とライセンスキーを確認します。</li>
<li>Web サーバーを再起動します。</li>
<li>お使いのシステムが互換性の要件を満たしていることを確認します。</li>
<li>INI 設定。</li>
</ul>
</td>
<td>
<ul>
<li><a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/not-seeing-data#apm-agents">New Relic ドキュメント/APM エージェント/データが表示されない</a></li>
<li><a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/not-seeing-data#browser-agent">New Relic ドキュメント/New Relic ブラウザー/データが表示されない</a></li>
<li><a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/not-seeing-data#infrastructure-agents">New Relic ドキュメント/New Relic インフラストラクチャ/データが表示されない</a></li>
<li><a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/not-seeing-data#mobile-agents">New Relic ドキュメント/New Relic Mobile/データが表示されない</a></li>
</ul>
</td>
</tr>
<tr>
<td>
<p><u>トランザクションのタイムスタンプに不一致があります。</u> New Relic UI を使用すると、長いトランザクションを（5 分以上）見つけるのに苦労する場合があります。 また、トランザクションが想定された時間枠外に表示される場合もあります。</p>
</td>
<td>
<p>New Relic UI には、トランザクションの開始時刻ではなく、トランザクションの終了時刻が表示されます。</p>
</td>
<td>
<p>New Relic UI を使用してトランザクションの開始を計算するには、トランザクションの期間を確認します。 New Relic UI で提供されるタイムスタンプ（トランザクションの終了）から期間を引きます。</p>
</td>
</tr>
<tr>
<td>
<p><u>NerdGraph GraphQL <code>curl</code> 特殊文字を使用したクエリ（例：） <code>|</code> および <code>%</code> 動作しない</u>.</p>
</td>
<td>
<p>New Relicの NerdGraph の「カールにコピー」機能には、現在、次のような特殊文字を処理する機能はありません <code>|</code> および <code>%</code>.</p>
</td>
<td>
<p>別の API ライブラリを使用して、特殊文字の問題を解決します。 例えば、Python で使用する Graphql API 用の GraphQLClient ライブラリや、Java 言語呼び出しを使用する Apache.commons などです。 に関するクライアントライブラリの確認 <a href="https://graphql.org/code/">GraphQL</a>.</p>
</td>
</tr>
<tr>
<td>
<p><u>グラフとダッシュボードの表示の問題。</u></p>
</td>
<td>
<p>New Relic ドメインをブラウザーに追加するか、許可リストー拡張機能をアンインストールして、不足しているグラフを解決し、問題を解決します。</p>
</td>
<td>
<p><a href="https://docs.newrelic.com/docs/apm/new-relic-apm/troubleshooting/charts-missing-or-do-not-render">New Relic ドキュメント / グラフが見つからない、または表示されない</a> </p>
</td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" colspan="3">PHP エージェントの問題</td>
</tr>
<tr>
<td>
<p><u>PHP エージェントが正しいインスタンス数を表示しません。</u></p>
</td>
<td>
<p>インスタンスの数は、バックエンドプロセスとスループットに応じて増える可能性があります。 サーバー値の違いは、一方のサーバーではプロセスが実行され、もう一方のサーバーでは実行されないことが原因である可能性があります。</p>
</td>
<td>
<p><a href="https://docs.newrelic.com/docs/agents/php-agent/troubleshooting/troubleshoot-php-agent-instance-count">New Relic ドキュメント &gt; PHP エージェントインスタンス数のトラブルシューティング</a> </p>
</td>
</tr>
</tbody>
</table>
