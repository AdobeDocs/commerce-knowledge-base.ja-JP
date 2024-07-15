---
title: エラ  [!DNL opensearch]  検索エンジンが存在しません。 フォールバック  [!DNL livesearch].
description: この記事では、「Error- [!DNL opensearch] search engine does't exist.」というエラーが表示される問題の解決策を説明します。 クラウドインフラストラクチャー上のAdobe Commerceにある  [!DNL livesearch].」にフォールバックします。
feature: Deploy, Search
role: Developer
exl-id: a6cc981d-b8f0-402d-8771-60d2f21f09f8
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# 検索エンジン [!DNL opensearch] エラーが存在しません。 [!DNL livesearch] にフォールバック。

この記事では、次のエラーが表示される問題の解決策を提供します。*エラー：検索エンジン [!DNL opensearch] 存在しません。 [!DNL livesearch] にフォールバック。[!DNL Live Search] が使用されているクラウドインフラストラクチャのAdobe Commerceで* きます。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン
* [!DNL Live Search] がインストールされ、使用中です

## 問題

次のメッセージがログに表示されます（[!DNL New Relic] で観察可能）。
*エラー：検索エ [!DNL opensearch] ジンが存在しません。 [!DNL livesearch].* にフォールバック

## 解決策

1. `.magento.env.yaml` ファイルを変更します。
1. 次の行を探します。

   ```yaml
     deploy:
   ...
       SEARCH_CONFIGURATION:
         engine: opensearch
   ```

1. これらの行がない場合は、`.magento.env.yaml` ファイルに追加します。
1. これらの行が存在する場合は、*[!DNL opensearch]* から *[!DNL livesearch]* に **エンジンを変更** します。
1. 変更をコミットしてから、再デプロイします。

## 関連資料

* ライブ検索ガイドの [ インストール  [!DNL Live Search]](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html)
