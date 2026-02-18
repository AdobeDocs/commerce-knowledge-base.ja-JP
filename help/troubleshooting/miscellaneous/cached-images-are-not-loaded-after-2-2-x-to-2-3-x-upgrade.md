---
title: キャッシュされたイメージが 2.2.X から 2.3.X へのアップグレード後にロードされない
description: この記事では、Cloud Infrastructure 2.2.X 上のAdobe Commerceから 2.3.X にアップグレードした後、キャッシュされた画像が表示されない問題の解決策を説明します。
exl-id: 3e6bd5aa-bd5d-4880-8b78-64f280647abe
feature: Cache, Upgrade
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# キャッシュされたイメージが 2.2.X から 2.3.X へのアップグレード後にロードされない

この記事では、Cloud Infrastructure 2.2.X 上のAdobe Commerceから 2.3.X にアップグレードした後、キャッシュされた画像が表示されない問題の解決策を説明します。

## 影響を受けるバージョンとエディション：

* Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ 2.2.X、2.3.X

## 問題

Adobe Commerceを 2.2.X から 2.3.X にアップグレードすると、キャッシュされた商品画像は使用できなくなり、代わりに 404 ページが表示されます。

この問題は、`.magento.app.yaml` に設定された Nginx の設定が正しくないことが原因です。`index.php` の代わりに `"/media"` の場所に `passthru: /get.php` （またはなし）が使用されます。

## 解決策

1. `.magento.app.yaml` の場所にある `"/media"` 設定ファイルを確認します。 正しい設定は次のようになります。

   ```yaml
   "/media":
       root: "pub/media"
       allow: true
       scripts: false
       expires: 1y
       passthru: "/get.php"
   ```

1. `passthru` が `"/get.php"` に設定されておらず、`expires` も設定されていない場合は、次の手順に従います。
1. 設定ファイルを修正します。
   * スタータープラン：自分でファイルを修正し、変更をプッシュします。
   * Pro プラン：
   * 統合：自分でファイルを修正して、変更をプッシュします。
   * ステージングと実稼動：自分でファイルを修正し、変更をプッシュし、[Adobe Commerce サポートチケットを作成して &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide) 適用させます。

1. <https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization> の説明に従って、Commerce Admin で Fastly 画像の最適化を有効にします（Fastly は事前に設定する必要があります）。

設定が正しいにもかかわらず問題が解決しない場合は、調査を続行するか、[Adobe Commerce サポート &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide) にお問い合わせください。
