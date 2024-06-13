---
title: キャッシュされたイメージが 2.2.X から 2.3.X へのアップグレード後にロードされない
description: この記事では、Cloud Infrastructure 2.2.X 上のAdobe Commerceから 2.3.X にアップグレードした後、キャッシュされた画像が表示されない問題の解決策を説明します。
exl-id: 3e6bd5aa-bd5d-4880-8b78-64f280647abe
feature: Cache, Upgrade
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# キャッシュされたイメージが 2.2.X から 2.3.X へのアップグレード後にロードされない

この記事では、Cloud Infrastructure 2.2.X 上のAdobe Commerceから 2.3.X にアップグレードした後、キャッシュされた画像が表示されない問題の解決策を説明します。

## 影響を受けるバージョンとエディション：

* Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ 2.2.X、2.3.X

## 問題

Adobe Commerceを 2.2.X から 2.3.X にアップグレードすると、キャッシュされた商品画像は使用できなくなり、代わりに 404 ページが表示されます。

この問題は、で設定された Nginx 設定が正しくないことが原因です `.magento.app.yaml`: `index.php` は（またはなにも）使用されません `"/media"` 場所 `passthru: /get.php`.

## 解決策

1. を確認 `.magento.app.yaml` 設定ファイル（） `"/media"` 場所。 正しい設定は次のようになります。

   ```yaml
   "/media":
       root: "pub/media"
       allow: true
       scripts: false
       expires: 1y
       passthru: "/get.php"
   ```

1. 次の場合 `passthru` はに設定されていません `"/get.php"` および `expires` が設定されていない場合は、次の手順を実行します。
1. 設定ファイルを修正します。
   * スタータープラン：自分でファイルを修正し、変更をプッシュします。
   * Pro プラン：
   * 統合：自分でファイルを修正して、変更をプッシュします。
   * ステージングと実稼動：自分でファイルを修正し、変更をプッシュして、 [Adobe Commerce サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) 適用する。

1. の説明に従って、Commerce Admin で Fastly 画像の最適化を有効にします（Fastly を事前に設定する必要があります）。 <https://devdocs.magento.com/guides/v2.3/cloud/cdn/fastly-image-optimization.html>.

設定が正しいにもかかわらず、まだ問題が発生している場合は、調査または問い合わせを続行します [Adobe Commerce サポート](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).
