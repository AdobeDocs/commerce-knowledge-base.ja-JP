---
title: エラー [!DNL opensearch] 検索エンジンが存在しません。 ～に戻る [!DNL livesearch].
description: この記事では、「Error- [!DNL opensearch] 検索エンジンが存在しません。 ～に戻る [!DNL livesearch].'、クラウドインフラストラクチャー上のAdobe Commerceにあります。
feature: Deploy, Search
role: Developer
exl-id: a6cc981d-b8f0-402d-8771-60d2f21f09f8
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# エラー [!DNL opensearch] 検索エンジンが存在しません。 ～に戻る [!DNL livesearch].

この記事では、次のエラーが表示される問題の解決策を説明します。 *エラー： [!DNL opensearch] 検索エンジンが存在しません。 ～に戻る [!DNL livesearch].* クラウドインフラストラクチャー上のAdobe Commerceで次の操作を行います [!DNL Live Search] が使用されます。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン
* [!DNL Live Search] インストール済みで使用中

## 問題

次のメッセージがログに表示されます（ [!DNL New Relic]）:
*エラー： [!DNL opensearch] 検索エンジンが存在しません。 ～に戻る [!DNL livesearch].*

## 解決策

1. を変更する `.magento.env.yaml` ファイル。
1. 次の行を探します。

   ```yaml
     deploy:
   ...
       SEARCH_CONFIGURATION:
         engine: opensearch
   ```

1. これらの行がない場合は、に追加します `.magento.env.yaml` ファイル。
1. これらの行が存在する場合、 **エンジンの変更** から *[!DNL opensearch]* 対象： *[!DNL livesearch]*.
1. 変更をコミットしてから、再デプロイします。

## 関連資料

* [インストール [!DNL Live Search]](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html) ライブ検索ガイドの
