---
title: セキュリティ スキャン ツール レポートが空白です
description: この記事では、実際のレポートではなく、セキュリティスキャンツールに空白ページが表示される問題の修正を説明します。 この問題を解決するには、ツールで使用するIPをファイアウォールのファイアウォール許可リストに追加する必要がある場合があります。
exl-id: e5f7f8c6-2dd3-44e3-8d19-f1f38d06dd6c
feature: Compliance, Security
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%
---
# セキュリティ スキャン ツール レポートが空白です

この記事では、実際のレポートではなく、セキュリティスキャンツールに空白ページが表示される問題の修正を説明します。 この問題を解決するには、ツールで使用するIPをファイアウォールのファイアウォール許可リストに追加する必要がある場合があります。

## 影響を受ける製品とバージョン：

* Adobe Commerce（すべてのデプロイメント方法）およびMagento Open Source（すべてのバージョン）

## イシュー

<u>複製する手順</u>:

1. ユーザーガイドの[ セキュリティスキャン ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan)の説明に従って、Web サイトを確認するようにセキュリティスキャンツールを設定します。
1. 「アクション」列で、「**スキャンを実行**」を選択します。

<u>期待される結果</u>:

レポート完了通知とレポートを開く機能を表示します。

<u>実際の結果</u>:

通知もレポートも利用できません。

## 原因

セキュリティスキャンツールがweb サイトに到達できなかったため、この問題が発生する可能性があります。 これは、Web サイトがダウンしてアクセスできないか、セキュリティスキャンツールがブロックされていることを意味します。

## Solution

web サイトを開いてみます。

* ページの読み込みが正常に完了した場合は、セキュリティスキャンツールで使用するIPをファイアウォールのファイアウォール許可リストに追加する必要がある場合があります。 次のIPが使用されます：52.87.98.44、34.196.167.176、3.218.25.102 （ポート 80および443）。
* サイトが読み込まれず、*「リクエストの処理中にエラーが発生しました」* メッセージが返される場合は、Web サイトでエラーの可能性がないか確認してください。

## 関連トピックス

* [本番稼働し、開発者向けドキュメントで](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview)を起動します。
* ユーザーガイドの[ セキュリティスキャン ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan)。
