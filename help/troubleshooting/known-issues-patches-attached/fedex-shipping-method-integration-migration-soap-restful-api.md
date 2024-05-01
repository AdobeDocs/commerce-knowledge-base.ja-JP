---
title: '''[!DNL FedEx] soap から RESTful API への発送方法の統合の移行'
promoted: true
description: に対処するためのパッチを適用する [!DNL FedEx] Adobe Commerce 2.4.4-p4 - 2.4.6-pX の SOAP から RESTful API への出荷方法の統合の移行。
feature: Shipping/Delivery
role: Developer
exl-id: 7e11a171-6924-41d0-a5c7-7b794d0da84c
source-git-commit: 7c468583883789a6bc6e41d1a787a356ea3205c4
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# [!DNL FedEx] soap から RESTful API への発送方法の統合の移行

この記事では、の問題を解決するためのパッチを提供します [!DNL FedEx] Adobe Commerce 2.4.4-p4 - 2.4.6-pX の SOAP から RESTful API への出荷方法の統合の移行。

[!DNL FedEx Web Services] トラッキング、住所の検証、郵便番号の検証 Web サービス定義言語（WSDLS）は、2024 年 5 月 15 日（PT）に廃止されます。 SOAP ベース [!DNL FedEx Web Services] は開発抑制の対象であり、に置き換えられました [!DNL FedEx] RESTFUL API。 詳しくは、次を参照してください [[!DNL FedEx Web Services]](https://www.fedex.com/en-us/developer/web-services.html).

この変更は現在のに影響します [!DNL FedEx] Adobe Commerceにおける shipping method integration の実装。現在の実装を修正し、非推奨の SOAP API から最新の API に移行する必要があります。 [!DNL FedEx] RESTFUL API。

2024 年 5 月 15 日（PT）以降、Adobe Commerceのお客様はアドビのサービスを利用できなくなります [!DNL FedEx] 発送方法の統合により、Adobeでは、Adobe Commerce 2.4.4 以降のお客様が最新のを使用できるようにするこのホットフィックスをリリースしました [!DNL FedEx] 非推奨（廃止予定）の SOAP API ではなく、RESTFUL API


## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe CommerceとオンプレミスおよびMagento Open Source:

* 2.4.4-p4
* 2.4.5
* 2.4.5-pX
* 2.4.6
* 2.4.6-pX

## 原因：

この [!DNL FedEx] soap ベースの API を非推奨（廃止予定）にし、代わりに RESTful API に置き換えました。 こちらを参照してください [[!DNL FedEx Web Services]](https://www.fedex.com/en-us/developer/web-services.html).

## 解決策

Adobe CommerceまたはMagento Open Sourceのバージョンに応じて、次のパッチを添付して使用します。

2.4.4 以降、2.4.5 以降、2.4.6 以降のバージョンでこの問題を解決するには、以下のAdobe Commerce/Magento Open Sourceのバージョンに対応するパッチを適用する必要があります。

## パッチ

Adobe CommerceまたはMagento Open Sourceのバージョンに応じて、次のパッチを添付して使用します。

### バージョン 2.4.4～p4 の場合：

* [FedexPatch-Composer-245p5-244p6develop.patch.zip](assets/FedexPatch-Composer-245p5-244p6develop.patch.zip)

### バージョン 2.4.5、2.4.5-pX の場合：

* [FedexPatch-Composer-245p5-244p6develop.patch.zip](assets/FedexPatch-Composer-245p5-244p6develop.patch.zip)


### バージョン 2.4.6、2.4.6-pX の場合：


* [FedexPatch-Composer-246p3develop.patch.zip](assets/FedexPatch-Composer-246p3develop.patch.zip)


## パッチの適用方法

ファイルを解凍し、以下を確認します [Adobeが提供する composer パッチの適用方法](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html) 手順については、サポートナレッジベースを参照してください。

## パッチが適用されているかどうかを知る方法

問題にパッチが適用されたかどうかを簡単に確認できないのであれば、そのパッチが正常に適用されたかどうかを確認することをお勧めします。 用途（例： *AC-9363*）をチェックするパッチとして使用します。

<u>これは、次の手順で実行できます</u>:

1. [のインストール [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html).
1. 次のコマンドを実行します。

   ```bash
   vendor/bin/magento-patches -n status |grep "9363|Status"
   ```

1. AC-9363 がを返す場合、次のような出力が表示されます *適用日* ステータス :

   ```bash
   ║ Id            │ Title                                                        │ Category        │ Origin                 │ Status      │ Details                                          ║ ║ N/A           │ ../m2-hotfixes/AC-9363_USPS_Ground_Advantage_shipping_method_COMPOSER_patch.patch      │ Other           │ Local                  │ Applied     │ Patch type: Custom                                
   ```
