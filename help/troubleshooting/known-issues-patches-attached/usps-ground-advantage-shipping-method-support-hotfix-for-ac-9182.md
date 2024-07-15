---
title: 'AC-9182 の [!DNL USPS] Ground Advantage 出荷方法サポートホットフィックス'
promoted: true
description: Adobe Commerce 2.4.4 - 2.4.6 [!DNL USPS] p2 の Ground Advantage 出荷方法の問題 AC-9182 に対処するためのパッチを適用します。
feature: Shipping/Delivery
role: Developer
exl-id: b6871d19-3d02-4026-82e6-3545f4ab7159
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# AC-9182 の [!DNL USPS] Ground Advantage 出荷方法サポートのホットフィックス

この記事では、Adobe Commerce 2.4.4 ～ 2.4.6-p2 の新しい **[!DNL USPS]Ground Advantage** の発送方法に関する問題 AC-9182 を修正するパッチを提供します。

2023 年 7 月 9 日（PT）に、米国郵便公社（[!DNL USPS]）は新しい配送方法 [[!DNL USPS] Ground Advantage](https://www.usps.com/ship/ground-advantage.htm) をリリースしました。

この新しい配送方法は、現在の 3 つの主な配送方法に代わるものです。

* [!DNL USPS] Retail Ground
* [!DNL USPS] ファーストクラスのパッケージサービス
* [!DNL USPS] 区画の選択地盤

[[!DNL USPS]  発表 ](https://faq.usps.com/s/article/USPS-Ground-Advantage#how_it_works)2023 年 9 月 30 日（PT）以降、これら 3 つの配送方法は廃止され、すべてのお客様は新しい **[!DNL USPS]Ground Advantage** 方法を使用する必要があります。

したがって、2023 年 9 月 30 日（PT）以降、USPS の配送方法を使用しているすべてのAdobe Commerce加盟店は、これら 3 つの従来の配送方法を使用して [!DNL USPS] から配送料を取得できなくなります。

この問題は、2.4.6-p3、2.4.5-p5、および 2.4.4-p6 のバージョンで、2023 年 10 月に予定されているセキュリティ専用パッチリリースの範囲で修正されます。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe CommerceとオンプレミスおよびMagento Open Source:

* 2.4.4
* 2.4.4-p1
* 2.4.4-p2
* 2.4.4-p3
* 2.4.4-p4
* 2.4.4-p5
* 2.4.5
* 2.4.5-p1
* 2.4.5-p2
* 2.4.5-p3
* 2.4.5-p4
* 2.4.6
* 2.4.6-p1
* 2.4.6-p2

## 原因：

[!DNL USPS] が [!DNL API] 更新を行いました。

## 解決策

2.4.4、2.4.5、および 2.4.6 バージョンでこの問題を解決するには、以下の AC-9182 パッチを適用する必要があります。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、次のリンクをクリックします。

[AC-9182_USPS_Ground_Advantage_shipping_method_COMPOSER_patch.zip](assets/AC-9182_USPS_Ground_Advantage_shipping_method_COMPOSER_patch.zip)

## パッチの適用方法

ファイルを解凍し、サポートナレッジベースで [Adobe提供の Composer パッチの適用方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html) を参照して手順を確認します。

## パッチが適用されているかどうかを知る方法

この問題にパッチが適用されたかどうかを簡単に確認できないので、AC-9182 パッチが正常に適用されたかどうかを確認することをお勧めします。

<u> これは、次の手順で実行できます </u>。

1. [ をインストールします  [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html)。
1. 次のコマンドを実行します。

   ```bash
   vendor/bin/magento-patches -n status |grep "9182|Status"
   ```

1. AC-9182 が *Applied* ステータスを返す場合、次のような出力が表示されます。

   ```bash
   ║ Id            │ Title                                                        │ Category        │ Origin                 │ Status      │ Details                                          ║ ║ N/A           │ ../m2-hotfixes/AC-9182_USPS_Ground_Advantage_shipping_method_COMPOSER_patch.patch      │ Other           │ Local                  │ Applied     │ Patch type: Custom                                
   ```
