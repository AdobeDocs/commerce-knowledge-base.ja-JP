---
title: デプロイメント後に表示されない画像の保存
description: この記事では、デプロイメント後に画像が正しく表示されない場合の解決策を提供します。
exl-id: 7e6bcebd-edff-437a-9103-2743443d2ed9
feature: Cache, Categories, Deploy, Storefront
role: Admin
source-git-commit: c4d586ca3980acbe4f33c5f2616ef7f3051bc7d3
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# デプロイメント後に表示されない画像の保存

この記事では、デプロイメント後に画像が正しく表示されない場合の解決策を提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x

## 問題

画像のサイズ変更を含むストアフロントテーマを使用する場合、デプロイ時に画像がカタログページに表示されたり表示されなくなったりしません。

## 原因：

これは、キャッシュから画像を読み込むことが原因で発生する場合があります。

## 解決策

このような場合は、Magentoコマンドを使用して画像キャッシュを再生成し、画像を適切に表示することができます。

これを実行するには、[Cloud Console](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html) から使用できる SSH 情報とストア URL が必要です。

1. [ データベースダンプ ](/help/how-to/general/create-database-dump-on-cloud.md) のソースとなったプロジェクトに SSH で接続します。詳しくは、開発者向けドキュメントの [ 環境への SSH](https://devdocs.magento.com/guides/v2.3/cloud/env/environments-ssh.html#ssh) を参照してください。
1. 次を実行して画像キャッシュを再生成します。

   ```bash
   php bin/magento catalog:images:resize
   ```

1. ストア URL を使用してカテゴリページをテストします。
