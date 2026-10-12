---
title: 異なるドメインの管理者とフロントからのサイバーソース支払いは処理されません
description: この記事では、ストアフロントとCommerce管理者の両方からサイバーソースの支払いを処理できない場合に関連する、既知のAdobe Commerce 2.3.0の制限に対するパッチを提供します。
exl-id: 948d5907-70bd-4890-bc8a-23e04b116018
feature: Admin Workspace, Orders, Payments
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: bb2df8be-afdd-4818-b6b5-95ca1dd3bc3a
    internal-label: Admin workspace
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%
---
# 異なるドメインの管理者とフロントからのサイバーソース支払いは処理されません

この記事では、ストアフロントとCommerce管理者の両方からサイバーソースの支払いを処理できない場合に関連する、既知のAdobe Commerce 2.3.0の制限に対するパッチを提供します。

>[!NOTE]
>
>Adobe Commerce Cybersourceのコア決済インテグレーションは2.3.3以降で廃止され、2.4.0で完全に削除されます。 代わりに、Marketplaceの[公式拡張機能](https://marketplace.magento.com/cybersource-global-payment-management.html)を使用してください。

## イシュー

以前のCybersource統合の実装では、1つのドメインからのみ支払いを処理できました。 その結果、Adobe Commerce ストアフロントがCommerce管理者とは異なるドメインにある場合、管理者でCybersourceを使用して注文を行おうとすると、次のエラーが発生します。「*X-Frame-Optionsによって拒否された読み込み：https://%your\_domain%/cybersource/SilentOrder/TokenResponse/ does not allow cross-origin framing.* ..&quot;

<u>複製する手順</u>:

1. 別のサブドメインに管理者を設定します。
1. **Stores**/設定/**Configuration**/**Sales**/**支払い方法**/**CyberSource**&#x200B;の下で、ストアのCybersourceを設定します。
1. **Sales** > **Orders**&#x200B;に移動します。
1. 新規注文を作成します。
1. 新規顧客の創出：
1. 顧客の詳細を入力します。
1. 注文の詳細（商品、配送方法）を入力します。
1. 支払い方法として「Cybersource」を選択します。
1. 送信します。

<u>期待される結果</u>：注文は問題なく行われます。

<u>実際の結果</u>：注文ページに読み込みアイコンが表示されますが、注文は行われません。 エラーがコンソールに表示されます。

## Solution

添付のパッチは、Cybersourceとの統合の改善を提供します。 パッチを適用したら、Adminで支払いを処理するためにCybersourceでプロファイルをもう1つ作成し、Commerce Adminの&#x200B;**Stores**/Settings > **Configuration** > **Sales** > **Payment Methods** > **CyberSource**&#x200B;で必要な資格情報をCybersource設定に追加する必要があります。

>[!NOTE]
>
>この改善は、Adobe Commerce オンプレミスおよびクラウドインフラストラクチャ 2.2.9および2.3.1に含まれています。

## パッチ

この記事には複数のパッチが添付されており、バージョンごとに異なるパッチが適用されます。 パッチをダウンロードするには、記事の最後までスクロールしてファイル名をクリックするか、次のリンクをクリックします。

* [MDVA-5914\_EE\_2.1.9\_COMPOSER\_v3.patchをダウンロード](assets/MDVA-5914_EE_2.1.9_COMPOSER_v3.patch.zip)
* [ダウンロード MDVA-8609\_EE\_2.2.2\_COMPOSER\_v2.patch](assets/MDVA-8609_EE_2.2.2_COMPOSER_v2.patch.zip)
* [MDVA-12964\_EE\_2.2.5\_COMPOSER\_v1.patchをダウンロード](assets/MDVA-12964_EE_2.2.5_COMPOSER_v1.patch.zip)
* [MDVA-16643\_EE\_2.3.0\_COMPOSER\_v1.patchをダウンロード](assets/MDVA-16643_EE_2.3.0_COMPOSER_v1.patch.zip)

## 互換性のあるAdobe Commerce バージョン

パッチは、パッチファイル名に記載されている特定のバージョン用に作成されました。 例えば、MDVA-5914\_EE\_2.1.9\_COMPOSER\_v3.patchはAdobe Commerce 2.1.9用に作成されたもので、このバージョンで使用するのに最適なパッチです。

パッチは次のバージョンとも互換性があります。

* Adobe Commerce オンプレミス 2.1.3-2.1.17、Adobe Commerce オンクラウドインフラストラクチャ 2.1.5-2.12 （MDVA-5914\_EE\_2.1.9\_COMPOSER\_v3.patch）
* Adobe Commerce オンプレミス 2.2.0-2.2.3、Adobe Commerce オンクラウドインフラストラクチャ 2.2.0-2.2.3 （MDVA-8609\_EE\_2.2.2\_COMPOSER\_v2.patch）
* Adobe Commerce オンプレミス 2.2.4-2.2.7、Adobe Commerce オンクラウドインフラストラクチャ 2.2.4-2.2.7 （MDVA-12964\_EE\_2.2.5\_COMPOSER\_v1.patch）
* Adobe Commerce オンプレミス 2.2.8、2.3.0、Adobe Commerce オンクラウドインフラストラクチャ 2.3.0 （MDVA-16643\_EE\_2.3.0\_COMPOSER\_v1.patch）

## パッチの適用方法

手順については、サポートナレッジベースの「[Adobeが提供するコンポーザーパッチを適用する方法](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/how-to-apply-a-composer-patch-provided-by-magento)」を参照してください。

## 添付ファイル
