---
title: 高度なレポート cron ジョブエラーAdobe Commerce
description: この記事では、高度なレポートにアクセスしようとするお客様に 404 エラーが発生する可能性がある、Adobe Commerceの高度なレポートの cron ジョブに関する問題のパッチを提供します。
exl-id: c11a5faf-a243-411a-af0f-585a401e6e39
feature: Cache
role: Developer
source-git-commit: 6287e708c830680e04dd068b64cf63ca13ecdedb
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 高度なレポート cron ジョブエラーAdobe Commerce

この記事では、高度なレポートにアクセスしようとするお客様に 404 エラーが発生する可能性がある、Adobe Commerceの高度なレポートの cron ジョブに関する問題のパッチを提供します。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメントオプション） 2.3.x

## 問題

お客様が詳細レポートにアクセスしようとすると、404 エラーが発生し、に関連付けられたログにエラーがあります `analytics_collect_data job` .

## 互換性のあるMagentoのバージョン：

パッチは、次のAdobe Commerceのバージョンとエディションと互換性があります（ただし、問題が解決しない可能性があります）。

* [MDVA-19391\_EE\_2.3.1\_COMPOSER\_v1.patch](assets/MDVA-19391_EE_2.3.1_COMPOSER_v1.patch.zip):Adobe Commerce（すべてのデプロイメントオプション） 2.3.1-2.3.4-p2
* [MDVA-18980\_EE\_2.2.6\_COMPOSER\_v1.patch](assets/MDVA-18980_EE_2.2.6_COMPOSER_v1.patch.zip):Adobe Commerce（すべてのデプロイメントオプション） 2.3.0
* [MDVA-15136\_EE\_2.2.6\_COMPOSER\_v1.patch](assets/MDVA-15136_EE_2.2.6_COMPOSER_v1.patch.zip):Adobe Commerce（すべてのデプロイメントオプション） 2.3.0

## **解決策**

この問題を修正するには、この記事に添付されている関連パッチを適用してください。 ダウンロードするには、次のリンクをクリックします。

* Download [MDVA-19391\_EE\_2.3.1\_COMPOSER\_v1.patch](assets/MDVA-19391_EE_2.3.1_COMPOSER_v1.patch.zip)
* Download [MDVA-15136\_EE\_2.2.6\_COMPOSER\_v1.patch](assets/MDVA-15136_EE_2.2.6_COMPOSER_v1.patch.zip)
* Download [MDVA-18980\_EE\_2.3.1\_COMPOSER\_v1.patch](assets/MDVA-18980_EE_2.2.6_COMPOSER_v1.patch.zip)

使用するパッチを確認するには、次の手順に従います。

<ol><li>次のコマンドを使用して、ログを確認します。<code>grep analytics_collect_data var/log/support_report.log var/log/support_report.log.1.gz</code>
</li><li>表示されるエラーに応じて、次の表の情報を使用してパッチを選択します。<table style="width: 826px;">
<tbody>
<tr>
<td class="wysiwyg-text-align-center">
<p>エラー</p>
</td>
<td class="wysiwyg-text-align-center">パッチ</td>
</tr>
<tr>
<td>
<pre>report.CRITICAL: cron ジョブ実行中のエラー {"exception":"[object] （RuntimeException （コード：0）: /srv/public_html/vendor/magento/module-cron/Observer/ProcessCronQueueObserver.php:327, TypeError （コード：0）: substr_count （）では、パラメーター 1 が文字列であることが想定されます。/srv/public_html/vendor/magento/module-page-builder-analytics/Model/ContentTypeUsageReportProvider.php:106）"} []</pre>または<pre>report.ERROR: Cron ジョブ analytics_collect_data にエラーがあります。substr_count （）は、パラメータ 1 が文字列であること、指定された null であることを想定しています。 統計：{"sum":0,"count":1,"realmem":0,"emalloc":0,"realmem_start":224919552,"emalloc_start":216398384}
  [] []</pre>
<p> </p>
</td>
<td>適用<a href="assets/MDVA-19391_EE_2.3.1_COMPOSER_v1.patch">MDVA-19391_EE_2.3.1_COMPOSER_v1.patch.zip</a>、キャッシュをクリアし、ジョブが再び実行されるまで 24 時間待ってから、もう一度試してください。</td>
</tr>
<tr>
<td>
<p><em>ファイル「/tmp/analytics/tmp/../tmp/../tmp/../tmp/../tmp/../tmp/../tmp/.../tmp/.../tmp/../tmp/.../tmp/.../tmp/.../tmp/.../tmp/.../tmp/.../tmp/.../tmp/.../tmp/../tmp/.../tmp/../tmp/../tmp/../tmp/../tmp/.../tmp/../tmp/</em></p>
</td>
<td>適用<a href="assets/MDVA-15136_EE_2.2.6_COMPOSER_v1.patch">MDVA-15136_EE_2.2.6_COMPOSER_v1.patch.zip</a>、キャッシュをクリアし、ジョブが再び実行されるまで 24 時間待ってから、もう一度試してください。</td>
</tr>
<tr>
<td><em>有効な暗号ではありません</em></td>
<td>適用<a href="assets/MDVA-18980_EE_2.2.6_COMPOSER_v1.patch">MDVA-18980_EE_2.2.6_COMPOSER_v1.patch.zip</a>、キャッシュをクリアし、ジョブが再び実行されるまで 24 時間待ってから、もう一度試してください。</td>
</tr>
</tbody>
</table>
</li></ol>

## パッチの適用方法

ファイルを解凍し、の指示に従います。 [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md).

## 関連資料

[ファイルを削除できません。 警告！リンク解除：管理からのファイルまたはディレクトリのエラーがありません](/help/troubleshooting/miscellaneous/file-cannot-be-deleated-no-file-or-directory.md)
