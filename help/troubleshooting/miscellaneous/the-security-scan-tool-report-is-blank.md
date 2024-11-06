---
title: セキュリティスキャンツールレポートが空白になる
description: この記事では、セキュリティスキャンツールで実際のレポートではなく空白ページが表示される問題の修正について説明します。 これを解決するには、ツールで使用される IP をファイアウォール許可リストに追加する必要がある可能性があります。
exl-id: e5f7f8c6-2dd3-44e3-8d19-f1f38d06dd6c
feature: Compliance, Security
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# セキュリティスキャンツールレポートが空白になる

この記事では、セキュリティスキャンツールで実際のレポートではなく空白ページが表示される問題の修正について説明します。 これを解決するには、ツールで使用される IP をファイアウォール許可リストに追加する必要がある可能性があります。

## 影響を受ける製品とバージョン：

* Adobe Commerce（すべてのデプロイメント方法）とMagento Open Source（すべてのバージョン）

## 問題

<u> 再現手順 </u>:

1. ユーザーガイドの [ セキュリティスキャン ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan) の説明に従って、セキュリティスキャンツールを設定して web サイトを確認します。
1. 「アクション」列で「**スキャンの実行**」を選択します。

<u> 期待される結果 </u>:

レポート完了通知と、レポートを開く機能を表示します。

<u> 実際の結果 </u>:

通知もレポートも利用できません。

## 原因：

この問題は、セキュリティ スキャン ツールが Web サイトに到達できなかったために発生する可能性があります。 つまり、Web サイトがダウンしてまったくアクセスできないか、セキュリティ スキャン ツールがブロックされています。

## 解決策

Web サイトを開いてみます。

* ページが正常に読み込まれた場合は、セキュリティ スキャン ツールが使用する IP をファイアウォール 許可リストに追加する必要がある可能性があります。 次の IP が使用されます。52.87.98.44、34.196.167.176、3.218.25.102 （ポート 80 および 443）。
* サイトが読み込まれず、「*リクエストの処理中にエラーが発生しました」* というメッセージが返された場合は、web サイトでエラーの可能性を確認します。

## 関連資料

* アドビの開発者向けドキュメントの [ 運用開始してローンチする ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview)。
* ユーザーガイドの [ セキュリティスキャン ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan)。
