---
title: ～に戻る [!DNL Elasticsearch7] 検索エンジンがに設定されている場合 [!DNL Opensearch]
description: この記事では、が*フォールバックする際の問題の解決策を説明します [!DNL Elasticsearch7]* error occurs when the search engine is set to [!DNL OpenSearch] Adobe Commerceで。
feature: Search
role: Developer
exl-id: 965d2929-5cf0-4e0a-9eed-6a656daaa120
source-git-commit: 6b8eecb3df0bb32344a5861a604a40402bb4d392
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# ～に戻る [!DNL Elasticsearch7] 検索エンジンがに設定されている場合 [!DNL Opensearch]

この記事では、次の場合の問題の解決策を説明します *～に戻る[!DNL Elasticsearch7]* 検索エンジンがに設定されているとエラーが発生する [!DNL OpenSearch] Adobe Commerceで。

## 影響を受けるバージョン

クラウドインフラストラクチャー上のAdobe Commerce 2.4.4 - 2.4.5

>[!NOTE]
>
>[!DNL OpenSearch] は、Adobe Commerce 2.4.6 以降の検索エンジンとして使用できます。

## 問題

を設定しました **検索エンジン** 対象： **[!DNL OpenSearch]**&#x200B;ただし、このタイプのエラーは `var/log/support_report.log` ファイル：

```[2024-04-04T00:27:41.212916+00:00] report.ERROR: opensearch search engine doesn't exist. Falling back to elasticsearch7 [] []```

<u>再現手順</u>:

1. を確認します。 [!DNL OpenSearch] は、次のコマンドを実行することによってインストールします。 `curl 127.0.0.1:9200`<br>
が示している場合 *1.2.4*、次に [!DNL OpenSearch] は既にインストールされています。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Catalog Search]**.
1. 検索エンジンを確認します。 次の内容が表示されます [!DNL Elasticsearch7].

## 原因：

はサポートしていますが、 [!DNL OpenSearch]を選択すると、アプリケーションは認識/同意するだけです [!DNL Elasticsearch7] を検索エンジンとして使用します。

Adobe Commerce バージョン 2.4.6 以降、アプリケーションはを許可するように更新されました [!DNL OpenSearch] を検索エンジンとして選択します。
に移動した場合 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Catalog Search]** クラウド以外の環境では、に示すように、このオプションを変更することができます。 **解決策** 下。
（メモ：クラウド環境では、検索エンジンが以下でロックされているので、このフィールドは変更できません。 `app/etc/env.php` ファイル。）

## 解決策

を更新 `SEARCH_CONFIGURATION` 内の変数 `.magento.env.yaml` ファイルを作成し、以下を実行します **検索エンジン** はに設定されています。 *[!DNL elasticsearch7]*.

## 関連資料

[OpenSearch サービスの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/opensearch.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。
