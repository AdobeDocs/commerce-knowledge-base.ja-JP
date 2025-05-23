---
title: Adobe Commerceで Site-Wide Analysis Tool にアクセスすると、403 エラーが発生する
description: この記事では、Adobe Commerceで Site-Wide Analysis Tool にアクセスしようとすると 403 エラーが発生した場合の解決策を提供します。
exl-id: f24fad17-62d6-4a0f-bcba-983c3dbee3d7
feature: Observability
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# Adobe Commerceで Site-Wide Analysis Tool にアクセスすると、403 エラーが発生する

この記事では、Adobe Commerceで Site-Wide Analysis Tool にアクセスしようとすると 403 エラーが発生した場合の解決策を提供します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー 2.4.1 以降でのAdobe Commerce。

## 問題

サイト全体の分析ツールにアクセスしようとすると、403 エラーが発生します。

<u> 再現手順：</u>

Commerce管理パネルにログインし、**レポート**/*システムインサイト*/**Site-Wide Analysis Tool** をクリックします。

<u> 期待される結果：</u>

Site-Wide Analysis Tool が表示されます。

<u> 実際の結果：</u>

*Error 403.* が表示されます。


## 解決策

Site-Wide Analysis Tool がアプリケーションに適切にアクセスできることを確認するには、CLI で次のコマンドを実行します。 `<store URL>` をストア URL に置き換えます。

```cURL
curl -sIL -X GET <store URL>/swat/key/index | grep HTTP
HTTP/2 403
```

取得した応答コードに応じて手順を実行します。

### 403 Forbidden 応答コード

応答コードが 403 の場合、Cloudflare ボット保護がサイト全体の分析ツールをブロックしている可能性があります。 ツールにアクセスするには、ツールの IP を許可リストに加えます。

* 107.23.33.174
* 3.225.9.244
* 3.88.83.85

### 200 応答コードと JSON 出力の修正

応答が正しい 200 コードと JSON 出力である場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) して、サイト全体の分析ツールへのアクセスに関する問題をエスカレーションします。


### 500 （致命的なエラー）応答コード

応答コードが 500 （Fatal error）の場合は、MDVA-38526 パッチをインストールしてください。 次のいずれかのリンクを使用して、必要なパッチのタイプに応じてパッチをダウンロードします。

* クラウドインフラストラクチャパッチ上のAdobe Commerce: [MDVA-38526_EE_2.4.1-p1_v3.patch.zip](assets/MDVA-38526_EE_2.4.1-p1_v3.patch.zip)
* クラウドインフラストラクチャコンポーザパッチ上のAdobe Commerce: [MDVA-38526_EE_2.4.1-p1_COMPOSER_v3.patch.zip](assets/MDVA-38526_EE_2.4.1-p1_COMPOSER_v3.patch.zip)

このパッチは、クラウドインフラストラクチャバージョン 2.4.1 以降のAdobe Commerceに適用されます。

### 応答が JSON ではない

応答出力が JSON でない場合は、PWA/ヘッドレスの実装が原因である可能性があります。 ヘッドレス実装を使用している場合は、Adobe Commerce オリジンへのリクエストをバイパスするように UPWARD 設定を更新します。 これを行うには、Adobe Commerce管理の **Stores**/**Configuration**/**General**/**Web**/**UPWARD PWA設定**/**フロント名^許可リスト** の下で、*swat* を追加します。

![Upward_configuration](assets/upward_pwa.png)

それでも Site-Wide Analysis Tool にアクセスできない場合、次回Commerce管理パネルにログインして **レポート**/*System Insights*/**Site-Wide Analysis Tool** に移動し、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) します。

## 関連資料

* [Site-Wide Analysis Tool ガイド ](https://experienceleague.adobe.com/docs/commerce-operations/tools/site-wide-analysis-tool/intro.html?lang=ja)
