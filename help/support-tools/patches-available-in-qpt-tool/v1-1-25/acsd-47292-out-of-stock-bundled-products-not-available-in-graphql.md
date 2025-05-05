---
title: 「ACSD-47292：在庫切れのバンドル製品は、GraphQL レスポンスでは使用できません」
description: ACSD-47292 パッチを適用すると、「在庫切れの商品を表示」が「はい」に設定されている場合でも、GraphQL レスポンスで在庫切れのバンドル商品が利用できないAdobe Commerceの問題を修正できます。
exl-id: 377dc62f-d1cd-4292-b25d-53c498b772a9
feature: Admin Workspace, Categories, GraphQL, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# ACSD-47292：在庫切れのバンドル製品は、GraphQL response では使用できません

ACSD-47292 パッチは、[!UICONTROL Display Out-of-Stock Products] が *[!UICONTROL Yes]* に設定されている場合でも、GraphQL レスポンスで在庫切れのバンドル製品が使用できない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされている場合に使用できます。 パッチ ID は ACSD-47292 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫切れのバンドル製品は、[!UICONTROL Display Out-of-Stock Products] が *[!UICONTROL Yes]* に設定されている場合でも、GraphQLの応答では使用できません。

<u> 再現手順 </u>:

1. Adobe Commerce管理者/ **[!UICONTROL System]** / **[!UICONTROL Configuration]** / **[!UICONTROL Catalog]** / **[!UICONTROL Inventory]** に移動し、[!UICONTROL Display Out-of-Stock Products] を *[!UICONTROL Yes]* に設定します。
1. s1 と s2 という 2 つのシンプルな製品を作成します。
1. s1 が在庫切れで個別に表示されない、s2 が在庫切れで個別に表示されない状態にして、カテゴリに割り当てます。
1. 1 つ以上のオプション製品でバンドルされた製品を作成し、s1 と s2 をこのオプションに割り当てます（入力タイプは「RadioButton」）。
1. バンドルされた製品を保存し、カテゴリに割り当てます。
1. ストアフロントに移動して、このバンドルされた製品を開きます。 在庫切れオプション s1 がグレー表示されて表示されます。
1. GraphQL リクエストを送信します。

```GraphQL
{
  categoryList(filters: { ids: { in: ["3"] } }) {
    id
    name
    products(pageSize: 8, sort: { position: ASC }) {
      total_count
      items {
        id
        sku
        name
        ... on BundleProduct {
          url_key
          items {
            title
            sku
            options {
              quantity
              position
              is_default
              product {
                id
                name
                sku
              }
            }
          }
        }
      }
    }
  }
}
```

<u> 期待される結果 </u>:

s1 バンドルオプションは、[!UICONTROL Display Out-of-Stock Products] が *[!UICONTROL Yes]* に設定され、ストアフロントに表示されるので、GraphQLの応答に一覧表示されます。

<u> 実際の結果 </u>:

s1 バンドルオプションは、GraphQLの応答には表示されません。

```GraphQL
"items": [
                                {
                                    "title": "oo1",
                                    "sku": "bundle2",
                                    "options": [
                                        {
                                            "quantity": 1,
                                            "position": 2,
                                            "is_default": false,
                                            "product": {
                                                "id": 2,
                                                "name": "s2",
                                                "sku": "s2"
                                            }
                                        }
                                    ]
                                }
                            ]
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
