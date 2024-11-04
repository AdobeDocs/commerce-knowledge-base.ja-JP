---
title: '''Adobe Commerce 2.4.6-p8 での  [!DNL GraphQL] ''placeOrder'' [!DNL API]  に対する後方互換性のない変更'''
promoted: true
description: この記事では、以前の 2.4.6 パッチバージョンのように、「placeOrder」が予期されたエラー応答を返さない、既知のAdobe Commerce バージョン 2.4.6-p8 クラウドおよびオンプレミスの問題の  [!DNL GraphQL API]  パッチを提供します。 これにより、PWAのストアフロントやその他のベースのストアフロントを店舗に使用しているマーチャントのチェックアウ  [!DNL GraphQL API] エクスペリエンスが損なわれる可能性があります。
feature: Checkout, REST, GraphQL
role: Developer
source-git-commit: 01b79c75df34de20f1ff50ab40c0a8d608ffa779
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Adobe Commerce 2.4.6-p8 での [!DNL GraphQL] `placeOrder` [!DNL API] に対する後方互換性のない変更

この記事では、以前の 2.4.6 パッチバージョンで見られたように、`placeOrder` [!DNL GraphQL API] が予期されたエラー応答を返さない、既知のAdobe Commerce バージョン 2.4.6-p8 クラウドおよびオンプレミスの問題のパッチを提供します。 これにより、ストアにストアフロントやその他の [!DNL GraphQL API] ベースのストアフロントを使用してい [!DNL PWA] マーチャントのチェックアウトエクスペリエンスが損なわれる可能性があります。

>[!NOTE]
>
>パッチの適用で問題が発生した場合は、サポートサービスにお問い合わせください。

## 影響を受ける製品とバージョン

* Cloud 2.4.6-p8 のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.6-p8

## 問題

Adobe Commerce 2.4.6-p8 セキュリティ専用パッチでアップグレードした後、以前の 2.4.6 パッチバージョンで見られたように、[`placeOrder` [!DNL GraphQL API]](https://developer.adobe.com/commerce/webapi/graphql/schema/cart/mutations/place-order/) が予期されたエラー応答を返しません。 これにより、ストアにストアフロントやその他の [!DNL GraphQL API] ベースのストアフロントを使用してい [!DNL PWA] マーチャントのチェックアウトエクスペリエンスが損なわれる可能性があります。

<u> 再現手順 </u>:

エラー応答が予想される場所で `placeOrder` [!DNL GraphQL] リクエストを実行します。

<u> 期待される結果 </u>:

予期されるエラー応答を受け取る。

<u> 実際の結果 </u>:

期待されたエラー応答の代わりに成功した応答が返されますが、新しい `errors` キーは次のようになります。

```
{
    "data": {
        "placeOrder": {
            "order": null,
            "__typename": "PlaceOrderOutput"
        }
    }
}
```

## Adobe Commerce on Cloud およびAdobe Commerce オンプレミス ソフトウェアのソリューション

この問題を解決するには、パッチを適用します。
ダウンロードするには、次のリンクをクリックします。

[ac-13283-composer-patch.zip](assets/ac-13283-composer-patch.zip)

## パッチの適用方法

ファイルを解凍し、サポートナレッジベースで [Adobe提供の Composer パッチの適用方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html) を参照して手順を確認します。

## Adobe Commerce on Cloud マーチャントのみ – パッチが適用されているかどうかを確認する方法

問題にパッチが適用されたかどうかを簡単に確認することはできないので、そのパッチが正常に適用されたかどうかを確認することをお勧めします。

<u> これを行うには、次の手順に従い、サンプルファイル `VULN-27015-2.4.7_COMPOSER.patch` を使用します **例として</u>**。

1. [ をインストールします  [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html)。
1. 次のコマンドを実行します。<br>
   ![ac-13283-tell-if-patch-applied-code](assets/cve-2024-34102-tell-if-patch-applied-code.png)
1. VULN-27015 が *Applied* ステータスを返す、次のような出力が表示されます。

   ```bash
   ║ Id            │ Title                                                        │ Category        │ Origin                 │ Status      │ Details                                          ║ ║ N/A           │ ../m2-hotfixes/VULN-27015-2.4.7_COMPOSER_patch.patch      │ Other           │ Local                  │ Applied     │ Patch type: Custom                                
   ```

<!-- For Step 2:
     ```bash
    vendor/bin/magento-patches -n status |grep "27015\|Status"
     ```
-->

