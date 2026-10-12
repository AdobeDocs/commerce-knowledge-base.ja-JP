---
title: 2.2.Xから2.3.Xへのアップグレード後、キャッシュされた画像が読み込まれない
description: この記事では、クラウドインフラストラクチャ 2.2.Xから2.3.XにAdobe Commerceからアップグレードした後、キャッシュされた画像が表示されない問題の解決策を説明します。
exl-id: 3e6bd5aa-bd5d-4880-8b78-64f280647abe
feature: Cache, Upgrade
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%
---
# 2.2.Xから2.3.Xへのアップグレード後、キャッシュされた画像が読み込まれない

この記事では、クラウドインフラストラクチャ 2.2.Xから2.3.XにAdobe Commerceからアップグレードした後、キャッシュされた画像が表示されない問題の解決策を説明します。

## 影響を受けるバージョンとエディション：

* Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ 2.2.X、2.3.X

## イシュー

Adobe Commerceを2.2.Xから2.3.Xにアップグレードすると、キャッシュされた製品画像は使用できなくなり、代わりに404 ページが表示されます。

この問題は、`.magento.app.yaml`で設定されたNginx設定が正しくないことが原因で発生します。`passthru: /get.php`ではなく`"/media"`の場所に`index.php` （またはなし）が使用されています。

## Solution

1. `"/media"`の場所にある`.magento.app.yaml`設定ファイルを確認してください。 正しい設定は次のようになります。

   ```yaml
   "/media":
       root: "pub/media"
       allow: true
       scripts: false
       expires: 1y
       passthru: "/get.php"
   ```

1. `passthru`が`"/get.php"`に設定されておらず、`expires`が設定されていない場合は、次の手順を実行します。
1. 設定ファイルを修正します。
   * スタータープラン：自分でファイルを修正し、変更をプッシュします。
   * プロプラン：
   * 統合：ファイルを自分で修正し、変更をプッシュします。
   * ステージングと実稼動：自分でファイルを修正し、変更をプッシュして、[Adobe Commerce サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)を作成して適用します。

1. <https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization>の説明に従って、Commerce管理者でFastlyの画像の最適化を有効にします（Fastlyは事前に設定する必要があります）。

設定が正しくても問題が解決しない場合は、調査を続行するか、[Adobe Commerce サポート &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)にお問い合わせください。
