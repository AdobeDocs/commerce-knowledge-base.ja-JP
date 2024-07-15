---
title: 'SOAPから RESTful API への [!DNL FedEx] shipping method integration の移行'
promoted: true
description: Adobe Commerce 2.4.4-p4 - 2.4.6-pX のSOAPから RESTful API への  [!DNL FedEx] shipping method integration の移行に対処するためのパッチを適用します。
feature: Shipping/Delivery
role: Developer
exl-id: 7e11a171-6924-41d0-a5c7-7b794d0da84c
source-git-commit: 7c468583883789a6bc6e41d1a787a356ea3205c4
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# SOAPから RESTful API への [!DNL FedEx] 送方法の統合の移行

この記事では、SOAPからAdobe Commerce 2.4.4-p4 - 2.4.6-pX の RESTful API への [!DNL FedEx] Shipping Method integration の移行に関する問題を解決するためのパッチを提供します。

[!DNL FedEx Web Services] トラッキング、住所の検証、郵便番号の検証 Web サービス定義言語（WSDLS）は、2024 年 5 月 15 日（PT）に廃止されます。 SOAP ベースの [!DNL FedEx Web Services] は開発時に統合対象となり、[!DNL FedEx] の RESTFUL API に置き換えられました。 詳しくは、[[!DNL FedEx Web Services]](https://www.fedex.com/en-us/developer/web-services.html) を参照してください。

この変更は、Adobe Commerceにおける現在の [!DNL FedEx] shipping method integration の実装に影響を与え、現在の実装を修正して、廃止されたSOAP API から最新の [!DNL FedEx] RESTFUL API に移行する必要があります。

2024 年 5 月 15 日（PT）以降、Adobe Commerceのお客様は現在の [!DNL FedEx] 発送方式の統合を使用できなくなります。そのため、Adobeでは、Adobe Commerce 2.4.4 以降のお客様が、非推奨のSOAPの代わりに最新の [!DNL FedEx] RESTFUL API を使用できるようにするこのホットフィックスをリリースしています。


## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe CommerceとオンプレミスおよびMagento Open Source:

* 2.4.4-p4
* 2.4.5
* 2.4.5-pX
* 2.4.6
* 2.4.6-pX

## 原因：

[!DNL FedEx] はSOAP ベースの API を非推奨（廃止予定）にし、代わりに RESTful API に置き換えました。 [[!DNL FedEx Web Services]](https://www.fedex.com/en-us/developer/web-services.html) を参照。

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

ファイルを解凍し、サポートナレッジベースで [Adobe提供の Composer パッチの適用方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html) を参照して手順を確認します。

## パッチが適用されているかどうかを知る方法

問題にパッチが適用されたかどうかを簡単に確認できないのであれば、そのパッチが正常に適用されたかどうかを確認することをお勧めします。 チェックするパッチとして（例：*AC-9363*）を使用します。

<u> これは、次の手順で実行できます </u>。

1. [ をインストールします  [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html)。
1. 次のコマンドを実行します。

   ```bash
   vendor/bin/magento-patches -n status |grep "9363|Status"
   ```

1. AC-9363 が *Applied* ステータスを返す場合、次のような出力が表示されます。

   ```bash
   ║ Id            │ Title                                                        │ Category        │ Origin                 │ Status      │ Details                                          ║ ║ N/A           │ ../m2-hotfixes/AC-9363_USPS_Ground_Advantage_shipping_method_COMPOSER_patch.patch      │ Other           │ Local                  │ Applied     │ Patch type: Custom                                
   ```
