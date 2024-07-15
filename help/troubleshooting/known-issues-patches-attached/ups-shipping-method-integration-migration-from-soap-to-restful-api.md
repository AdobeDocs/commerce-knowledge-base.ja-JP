---
title: '[!DNL UPS] 出荷方法の統合を  [!DNL SOAP]  から  [!DNL RESTful API] に移行しました'
promoted: true
description: Adobe Commerce 2.4.4 ～ 2.4.6 [!DNL UPS] pX での  [!DNL SOAP] shipping method integration の from [!DNL RESTful API] to-migration に対処するためのパッチを適用します。
feature: Shipping/Delivery
role: Developer
exl-id: 8ab5d4a8-0155-4b2c-ab67-d0bd2f949a07
source-git-commit: 6694bb1e041e6285f5bd5a05a1c37b7062521f52
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# [!DNL SOAP] から [!DNL RESTful API] への [!DNL UPS] 送方法の統合の移行

>[!NOTE]
>
>**2024 年 6 月 6 日（PT）** より前にこの記事から 3 つのパッチをアップロードした場合：[!DNL Metric System/SI][!DNL Metric System/SI] の測定値（キログラムとセンチメートル）が使用されていないので、この問題が発生した場合は、この記事で公開されている新しいパッチの 1 つをAdobe Commerce/Magento Open Sourceの 2.4.4+/2.4.5+/2.4.6+用に再度適用する必要があります。そうしないと、**[!DNL Admin configuration]** の [!DNL UPS] 送方法で **キログラム** と **** センチメートルののの測定値を選択できなくなります。 これらの新しいパッチは、以前にリリースされたパッチと互換性があります。 この問題は、**2024 年 6 月 11 日（PT）** に予定されている今後のAdobe Commerce バージョン 2.4.7-p1 リリースの範囲で永続的に修正されます。

>[!NOTE]
>
>**2023 年 10 月 10 日（PT）** より前にこの記事から 3 つのパッチをアップロードした場合は、Adobe Commerce/Magento Open Sourceの 2.4.4+/2.4.5+/2.4.6+のバージョンに対して、この記事で公開されているパッチのいずれかを再度適用する必要があります。そうしないと、**[!DNL Admin configuration]** で特定の [!DNL UPS] 送方法を選択して設定できず、すべてを有効にする必要があるからです。 これらの新しいパッチは、以前にリリースされたパッチと互換性があります。

この記事では、Adobe Commerce 2.4.4 ～ 2.4.6-pX での [!DNL SOAP] から [!DNL RESTful API] への [!DNL United Parcel Service (UPS)] shipping method integration の移行に関する問題を解決するためのパッチを提供します。

[!DNL UPS API] セキュリティモデルの最新の更新に従って、[!DNL UPS] はすべての [!DNL APIs] ーザーに [!DNL OAuth 2.0] セキュリティモデルを実装し（詳細については、[[!DNL UPS]  開発者ポータルアクセスキー移行ガイド ](https://developer.ups.com/oauth-developer-guide?loc=en_US&amp;sp_rid=NTA5MzQ1OTE2NjEyS0&amp;sp_mid=72989914) を参照）、全体的なセキュリティを強化して詐欺を減らし、[!DNL API] 機能を強化しました。

この変更は、Adobe Commerceにおける現在の [!DNL UPS] shipping method integration の実装に影響を与えます。また、[!DNL OAuth 2.0] 認証プロトコルをサポートするには、現在の実装を修正し、[!DNL SOAP API] から [!DNL RESTful API] に移行する必要があります。

**2024 年 6 月以降**、Adobe Commerce マーチャントは、現在の [!DNL UPS] 統合と取引できなくなりました。そのため、このホットフィックスをリリースしています。これにより、Adobe Commerce 2.4.4 以降、2.4.5 以降、2.4.6 以降のマーチャントを最新の [!DNL UPS REST APIs] に移行できます。

この問題は、Adobe Commerce/Magento Open Sourceバージョン 2.4.7 で修正され、2023 年 10 月の 2.4.7-beta2 リリースにも含まれる予定です。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe CommerceとオンプレミスおよびMagento Open Source:

* 2.4.4
* 2.4.4-pX
* 2.4.5
* 2.4.5-pX
* 2.4.6
* 2.4.6-pX

## 原因

[!DNL UPS] は [ 彼らのためのセキュリティの更新  [!DNL API]](https://developer.ups.com/oauth-developer-guide?loc=en_US&amp;sp_rid=NTA5MzQ1OTE2NjEyS0&amp;sp_mid=72989914) をリリースしました。

発送元として欧州連合（EU）がある場合（他の発送元も同じ問題を経験する可能性があります）、[!DNL UPS REST] のリクエストでエラーが発生します。
「*1 つの出荷の単位として、KGS/IN、LBS/CM、または OZS/CM を使用することはできません。*」

## 解決策

Adobe CommerceまたはMagento Open Sourceのバージョンに応じて、次のパッチを添付して使用します。

2.4.4 以降、2.4.5 以降、2.4.6 以降のバージョンでこの問題を解決するには、以下のAdobe Commerce/Magento Open Sourceのバージョンに対応するパッチを適用する必要があります。

## パッチ

Adobe CommerceまたはMagento Open Sourceのバージョンに応じて、次のパッチを添付して使用します。

### バージョン 2.4.4、2.4.4-pX の場合：

* [AC-11984_UPS_Shipping_Method_Migration_REST_API_2.4.4x_COMPOSER.patch.zip](assets/AC-11984_UPS_Shipping_Method_Migration_REST_API_2.4.4x_COMPOSER.patch.zip)

### バージョン 2.4.5、2.4.5-pX の場合：

* [AC-11983_UPS_Shipping_Method_Migration_REST_API_2.4.5x_COMPOSER.patch.zip](assets/AC-11983_UPS_Shipping_Method_Migration_REST_API_2.4.5x_COMPOSER.patch.zip)

### バージョン 2.4.6、2.4.6-pX の場合：

* [AC-11916_UPS_Shipping_Method_Migration_REST_API_2.4.6x_COMPOSER.patch.zip](assets/AC-11916_UPS_Shipping_Method_Migration_REST_API_2.4.6x_COMPOSER.patch.zip)

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
