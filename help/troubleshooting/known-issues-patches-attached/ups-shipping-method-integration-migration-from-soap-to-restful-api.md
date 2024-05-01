---
title: '[!DNL UPS] からの発送方法の統合の移行 [!DNL SOAP] 対象： [!DNL RESTful API]'
promoted: true
description: に対処するためのパッチを適用する [!DNL UPS] からの発送方法の統合の移行 [!DNL SOAP] 対象： [!DNL RESTful API] Adobe Commerce 2.4.4 - 2.4.6-pX の場合。
feature: Shipping/Delivery
role: Developer
exl-id: 8ab5d4a8-0155-4b2c-ab67-d0bd2f949a07
source-git-commit: 7785a37e033bc2bea5b6a1509c337289e7b871cb
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# [!DNL UPS] からの発送方法の統合の移行 [!DNL SOAP] 対象： [!DNL RESTful API]

>[!NOTE]
>
>この記事の 3 つのパッチのいずれかを事前にアップロードした場合 **2023 年 10 月 10 日（Pt）**&#x200B;を参照してください。そうでない場合、特定のパッチを選択して設定することができないので、2.4.4+/2.4.5+/2.4.6+のバージョンのAdobe CommerceまたはMagento Open Sourceに対して、この記事で公開されているパッチのいずれかを再度適用する必要があります [!DNL UPS] での発送方法 **[!DNL Admin configuration]**&#x200B;を有効にするには、それらをすべて有効にする必要があります。 これらの新しいパッチは、以前にリリースされたパッチと互換性があります。

この記事では、の問題を解決するためのパッチを提供します [!DNL United Parcel Service (UPS)] からの発送方法の統合の移行 [!DNL SOAP] 対象： [!DNL RESTful API] Adobe Commerce 2.4.4 - 2.4.6-pX の場合。

の最新の更新内容によると [!DNL UPS API] セキュリティモデル [!DNL UPS] 実装済み [!DNL OAuth 2.0] すべてのユーザーのセキュリティ モデル [!DNL APIs] （詳しくは、 [[!DNL UPS] 開発者ポータルアクセスキー移行ガイド](https://developer.ups.com/oauth-developer-guide?loc=en_US&amp;sp_rid=NTA5MzQ1OTE2NjEyS0&amp;sp_mid=72989914)）を使用して、セキュリティ全体を強化し、不正を減らし、強化を実現します。 [!DNL API] の機能。

この変更は現在のに影響します [!DNL UPS] Adobe Commerceでの shipping method integration の実装。現在の実装を修正し、から移行する必要があります。 [!DNL SOAP API] に [!DNL RESTful API] 支えることができる [!DNL OAuth 2.0] 認証プロトコル。

**2024 年 6 月より**、Adobe Commerceのマーチャントは、当社の現在のサービスと取引できなくなります [!DNL UPS] そのため、このホットフィックスをリリースする予定です。これにより、Adobe Commerce 2.4.4 以降/2.4.5 以降/2.4.6 以降のマーチャントを最新のバージョンに移行できます。 [!DNL UPS REST APIs].

この問題は、Adobe Commerce/Magento Open Sourceバージョン 2.4.7 で修正され、2023 年 10 月の 2.4.7-beta2 リリースにも含まれる予定です。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe CommerceとオンプレミスおよびMagento Open Source:

* 2.4.4
* 2.4.4-pX
* 2.4.5
* 2.4.5-pX
* 2.4.6
* 2.4.6-pX

## 原因：

この [!DNL UPS] リリース日： [ユーザーのセキュリティ更新 [!DNL API]](https://developer.ups.com/oauth-developer-guide?loc=en_US&amp;sp_rid=NTA5MzQ1OTE2NjEyS0&amp;sp_mid=72989914).

## 解決策

Adobe CommerceまたはMagento Open Sourceのバージョンに応じて、次のパッチを添付して使用します。

2.4.4 以降、2.4.5 以降、2.4.6 以降のバージョンでこの問題を解決するには、以下のAdobe Commerce/Magento Open Sourceのバージョンに対応するパッチを適用する必要があります。

## パッチ

Adobe CommerceまたはMagento Open Sourceのバージョンに応じて、次のパッチを添付して使用します。

### バージョン 2.4.4、2.4.4-pX の場合：

* [AC-9363_UPS_Shipping_Method_Migration_REST_API_2.4.4x_COMPOSER.patch.zip](assets/AC-9646_UPS_Shipping_Method_Migration_REST_API_2.4.4x_COMPOSER.patch.zip)

### バージョン 2.4.5、2.4.5-pX の場合：

* [AC-9358_UPS_Shipping_Method_Migration_REST_API_2.4.5x_COMPOSER.patch.zip](assets/AC-9647_UPS_Shipping_Method_Migration_REST_API_2.4.5x_COMPOSER.patch.zip)

### バージョン 2.4.6、2.4.6-pX の場合：

* [AC-9345_UPS_Shipping_Method_Migration_REST_API_2.4.6x_COMPOSER.patch.zip](assets/AC-9648_UPS_Shipping_Method_Migration_REST_API_2.4.6x_COMPOSER.patch.zip)

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
