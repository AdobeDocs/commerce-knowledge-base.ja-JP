---
title: 展開後に表示されない画像を保存する
description: この記事では、デプロイメント後に画像が正しく表示されない場合の解決策を提供します。
exl-id: 7e6bcebd-edff-437a-9103-2743443d2ed9
feature: Cache, Categories, Deploy, Storefront
role: Admin
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
    internal-label: Categories
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%
---
# 展開後に表示されない画像を保存する

この記事では、デプロイメント後に画像が正しく表示されない場合の解決策を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure 2.2.x、2.3.x

## イシュー

画像のサイズを変更してストアフロントのテーマを使用する場合、デプロイ時にカタログページに画像が表示されたり表示されたりすることはありません。

## 原因

これは、キャッシュから画像が読み込まれたために発生する可能性があります。

## Solution

このような場合は、Magento コマンドを使用して画像キャッシュを再生成し、画像を適切に表示できます。

これを実行するには、[Cloud Console](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html?lang=ja)を通じて利用可能なSSH情報とストア URLが必要です。

1. [&#x200B; データベースダンプ &#x200B;](/help/how-to/general/create-database-dump-on-cloud.md)のソースであったプロジェクトへのSSH。詳しくは、開発者ドキュメントの[環境へのSSH](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/secure-connections)を参照してください。
1. 次のコマンドを実行して、画像キャッシュを再生成します。

   ```bash
   php bin/magento catalog:images:resize
   ```

1. ストア URLを使用してカテゴリーページをテストします。
