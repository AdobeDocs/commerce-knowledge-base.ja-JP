---
title: 「ACSD-50794:GraphQL経由でお客様の注文からギフトラッピングを削除できない」
description: ACSD-50794 パッチを適用すると、GraphQLを介してお客様の注文からギフトラッピングを削除できないAdobe Commerceの問題を修正できます。
exl-id: 4983910c-9ea0-451e-a2b6-81485184bbce
feature: Gift, GraphQL, Orders
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# ACSD-50794:GraphQL経由でお客様の注文からギフトラッピングを削除できない

ACSD-50794 パッチを使用すると、GraphQL経由でお客様の注文からギフトラッピングを削除できない問題が修正されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.32 がインストールされています。 パッチ ID は ACSD-50794 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQLを使用して、お客様の注文からギフト包装を削除することはできません。

<u>再現手順</u>:

1. フロントエンドから顧客を作成します。
1. シンプルな製品を作成します。
1. Enable （有効） *[!UICONTROL Gift Messages]* ～に行くことによって **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Gift Options]** およびを設定 *[!UICONTROL Allow Gift Messages]* = *[!UICONTROL Yes]*.
1. 作成 *[!UICONTROL Gift Wrapping]* ～に行くことによって **[!UICONTROL Stores]** > **[!UICONTROL Other Settings]** > **[!UICONTROL Gift Wrapping]**.
1. 顧客トークンを取得します。
1. 空の買い物かごである customerCart を作成します。
   * 商品を買い物かごに追加します。 `addProductsToCart` 突然変異
   * 請求先住所の設定： `setBillingAddressOnCart` 突然変異
   * 配送先住所の設定： `setShippingAddressesOnCart` 突然変異
   * 出荷方法の設定： `setShippingMethodsOnCart` 突然変異（flatrate）
   * 支払方法の設定： `setPaymentMethodOnCart` 突然変異（checkmo）
1. 今すぐギフト包装をチェック *Uid* この買い物かごクエリを使用すると、

   <pre><code class="language-GraphQL">
    {
      cart(cart_id: "{{CART_ID}}") {
        available_gift_wrappings{
            uid
        }
    }
    }
    </code></pre>

1. ギフトラップの設定 `setGiftOptionsOnCart`.
1. 買い物かご：買い物かごクエリを確認します。
1. 次を使用してギフト ラップの設定を解除 `setGiftOptionsOnCart` （値を null に設定）。
1. もう一度、cart:cart クエリを確認します。
1. 注文： `placeOrder` 変異。
1. 顧客クエリ「customer」を実行します。

   <pre><code class="language-graphql">
    query {
      customer {
        firstname
        middlename
        lastname
        suffix
        email
        orders {
            items {
                order_date
                gift_wrapping {
                    design
                    uid
                }
            }
        }
        addresses {
          firstname
          middlename
          lastname
          street
          city
          region {
            region_code
            region
          }
          postcode
          country_code
          telephone
        }
      }
    }
    </code></pre>

<u>期待される結果</u>:

ユーザーがギフトラップを設定して設定解除すると、顧客クエリは null を返します。

<u>実際の結果</u>:

顧客クエリは、適用されたとおりにギフトラッピングを返します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
