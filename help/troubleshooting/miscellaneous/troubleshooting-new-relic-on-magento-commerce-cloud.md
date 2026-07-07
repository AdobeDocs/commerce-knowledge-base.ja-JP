---
title: Adobe Commerce上のNew Relic クラウドインフラストラクチャのトラブルシューティング
description: この記事では、Adobe Commerce上のNew Relic クラウドインフラストラクチャのトラブルシューティングに関するリソースを提供します。
exl-id: ea763291-5c9b-4575-b2ee-820dbc367743
feature: Cloud, Observability, Paas
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Adobe Commerce上のNew Relic クラウドインフラストラクチャのトラブルシューティング

この記事では、Adobe Commerce上のNew Relic クラウドインフラストラクチャのトラブルシューティングに関するリソースを提供します。

<table>
<tbody>
<tr>
<td class="wysiwyg-text-align-center"><strong>イシュー</strong></td>
<td class="wysiwyg-text-align-center"><strong>原因</strong></td>
<td class="wysiwyg-text-align-center"><strong>リソース</strong></td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" colspan="3">アクセスの問題</td>
</tr>
<tr>
<td>
<p><u>New Relicでプロジェクトを表示できません。</u></p>
<p><em>New Relic</em>にログインしますが、表示/アクセス権を持つ必要があるプロジェクトが表示されません。</p>
</td>
<td>
<p>このような場合、管理者ユーザーがプロジェクトにユーザーを追加する必要があります。</p>
</td>
<td>
<p><a href="https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/faq/access-new-relic-services.html?lang=ja"> サポートナレッジベースのNew Relic サービス </a>へのアクセス。</p>
</td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" colspan="3">データの問題</td>
</tr>
<tr>
<td>
<p><u>インストール後にデータが見つかりません。</u></p>
<p><a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/new-relic-diagnostics">New Relic診断ユーティリティ </a>を使用して、原因の特定を試みます。 これが役に立たない場合は、エージェント固有の解決策を確認してください。 これらのソリューションを含む記事へのリンクは、右側の列にあります。</p>
</td>
<td>
<p>欠落しているデータには、さまざまな原因がある可能性があります。 次のようなものがあります。</p>
<ul>
<li>エージェントがインストールされていることを確認します。</li>
<li>アプリの名前とライセンスキーを確認します。</li>
<li>Web サーバーを再起動します。</li>
<li>お使いのシステムが互換性の要件を満たしていることを確認してください。</li>
<li>INI設定：</li>
</ul>
</td>
<td>
<ul>
<li><a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/not-seeing-data#apm-agents">New Relic ドキュメント &gt; APM Agents &gt; データが表示されない</a></li>
<li><a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/not-seeing-data#browser-agent">New Relic ドキュメント &gt; New Relic ブラウザー&gt; データが表示されない</a></li>
<li><a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/not-seeing-data#infrastructure-agents">New Relic ドキュメント &gt; New Relic インフラストラクチャ &gt; データが表示されない</a></li>
<li><a href="https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/not-seeing-data#mobile-agents">New Relic ドキュメント &gt; New Relic Mobile &gt; データが表示されない</a></li>
</ul>
</td>
</tr>
<tr>
<td>
<p><u> トランザクションのタイムスタンプの不一致。</u> New Relic UIを使用して、長いトランザクション（5分以上）を見つけるのに苦慮する場合があります。 また、予想される時間枠の外に表示されるトランザクションを見つけることもできます。</p>
</td>
<td>
<p>New Relic UIには、トランザクションの開始時間ではなく、トランザクションの終了時間が表示されます。</p>
</td>
<td>
<p>New Relic UIを使用してトランザクションの開始を計算するには、トランザクションの期間を確認します。 New Relic UIが提供するタイムスタンプ（トランザクションの終了）から期間の金額を差し引きます。</p>
</td>
</tr>
<tr>
<td>
<p><u>NerdGraph GraphQL <code>curl</code>のクエリで<code>|</code>や<code>%</code>などの特殊文字が使用されていますが、</u>は機能しません。</p>
</td>
<td>
<p>NerdGraph内のNew Relicの「curlにコピー」機能では、現在、<code>|</code>や<code>%</code>などの特殊文字を処理する方法を提供していません。</p>
</td>
<td>
<p>特殊文字を使用して問題を解決するには、別のAPI ライブラリを使用します。 例えば、Python上のGraphql API用GraphQLClient ライブラリ、Java言語呼び出しによるApache.commonsなどです。 <a href="https://graphql.org/code/">GraphQL</a>のクライアントライブラリを確認します。</p>
</td>
</tr>
<tr>
<td>
<p><u>チャートとダッシュボードの表示に関する問題。</u></p>
</td>
<td>
<p>New Relic ドメインをブラウザーに追加するか、許可リスト拡張機能をアンインストールして問題を引き起こして、欠落しているグラフを解決します。</p>
</td>
<td>
<p><a href="https://docs.newrelic.com/docs/apm/new-relic-apm/troubleshooting/charts-missing-or-do-not-render">New Relic ドキュメント/グラフが見つからないか、レンダリングされません</a> </p>
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
<p>インスタンスの数は、バックエンドプロセスとスループットによって増加する可能性があります。 サーバー値の違いは、一方のサーバーで実行されているプロセスが原因で発生する可能性がありますが、もう一方のサーバーでは発生しません。</p>
</td>
<td>
<p><a href="https://docs.newrelic.com/docs/agents/php-agent/troubleshooting/troubleshoot-php-agent-instance-count">New Relic ドキュメント &gt; PHP エージェントインスタンス数のトラブルシューティング </a> </p>
</td>
</tr>
</tbody>
</table>
