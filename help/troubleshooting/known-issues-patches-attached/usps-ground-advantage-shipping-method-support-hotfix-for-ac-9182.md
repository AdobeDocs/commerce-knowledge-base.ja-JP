---
title: '''[!DNL USPS] AC-9182''の Ground Advantage 出荷方法サポート ホットフィックス'
promoted: true
description: に対処するためのパッチを適用する [!DNL USPS] Adobe Commerce 2.4.4 - 2.4.6-p2 の Ground Advantage 出荷方法の問題。
feature: Shipping/Delivery
role: Developer
exl-id: b6871d19-3d02-4026-82e6-3545f4ab7159
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# [!DNL USPS] AC-9182 の Ground Advantage 出荷方法サポートのホットフィックス

この記事では、新しいの問題 AC-9182 を解決するためのパッチを提供します **[!DNL USPS]地上優位性** Adobe Commerceでの発送方法 2.4.4 - 2.4.6-p2。

2023 年 7 月 9 日（Pt）、United States Postal Service （[!DNL USPS]）が新しい出荷方法をリリースしました。 [[!DNL USPS] 地上優位性](https://www.usps.com/ship/ground-advantage.htm).

この新しい配送方法は、現在の 3 つの主な配送方法に代わるものです。

* [!DNL USPS] 小売基盤
* [!DNL USPS] ファーストクラスのパッケージサービス
* [!DNL USPS] 区画の選択地盤

[[!DNL USPS] 発表された](https://faq.usps.com/s/article/USPS-Ground-Advantage#how_it_works) 2023 年 9 月 30 日（PT）以降、これら 3 つの配送方法は廃止され、すべてのお客様は新しいを使用する必要があります **[!DNL USPS]地上優位性** その代わり、メソッドを使用します。

したがって、2023 年 9 月 30 日（PT）以降、USPS の配送方法を使用しているすべてのAdobe Commerce加盟店は、から配送料を取得できなくなります [!DNL USPS] これらの 3 つの従来の配送方法を使用する方法を使用します。

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

この [!DNL USPS] を作成 [!DNL API] 更新。

## 解決策

2.4.4、2.4.5、および 2.4.6 バージョンでこの問題を解決するには、以下の AC-9182 パッチを適用する必要があります。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、次のリンクをクリックします。

[AC-9182_USPS_Ground_Advantage_shipping_method_COMPOSER_patch.zip](assets/AC-9182_USPS_Ground_Advantage_shipping_method_COMPOSER_patch.zip)

## パッチの適用方法

ファイルを解凍し、以下を確認します [Adobeが提供する composer パッチの適用方法](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html) 手順については、サポートナレッジベースを参照してください。

## パッチが適用されているかどうかを知る方法

この問題にパッチが適用されたかどうかを簡単に確認できないので、AC-9182 パッチが正常に適用されたかどうかを確認することをお勧めします。

<u>これは、次の手順で実行できます</u>:

1. [のインストール [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html).
1. 次のコマンドを実行します。

   ```bash
   vendor/bin/magento-patches -n status |grep "9182|Status"
   ```

1. AC-9182 がを返す場合、次のような出力が表示されます *適用日* ステータス :

   ```bash
   ║ Id            │ Title                                                        │ Category        │ Origin                 │ Status      │ Details                                          ║ ║ N/A           │ ../m2-hotfixes/AC-9182_USPS_Ground_Advantage_shipping_method_COMPOSER_patch.patch      │ Other           │ Local                  │ Applied     │ Patch type: Custom                                
   ```
