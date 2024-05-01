---
title: '''ACSD-46519: [!UICONTROL product_count] 。対象： [!UICONTROL categoryList] [!DNL GraphQL] クエリがアンカーカテゴリの「0」を返す'
description: を使用する際のAdobe Commerceの問題を修正するために、ACSD-46519 パッチを適用します。 [!UICONTROL categoryList] [!DNL GraphQL] 子カテゴリを取得するメソッド。このメソッドは、 [!UICONTROL product_count] 親カテゴリには 0 を指定します。
exl-id: b71be3e6-6235-4e96-848b-d61eda973d98
feature: Categories, GraphQL, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# ACSD-46519: [!UICONTROL product_count] 。対象： [!UICONTROL categoryList] [!DNL GraphQL] クエリを実行すると、アンカーカテゴリに対して 0 が返される

ACSD-46519 パッチは、 [!UICONTROL product_count] 。対象： [!UICONTROL categoryList] [!DNL GraphQL] クエリを実行すると、アンカーカテゴリに対して 0 が返されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.23 がインストールされています。 パッチ ID は ACSD-46519 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

いつ [!UICONTROL categoryList] [!DNL GraphQL] メソッドは、が表示する子カテゴリの取得に使用されます。 [!UICONTROL product_count] 親カテゴリには 0 を指定します。

<u>再現手順</u>:

1. 以下を使用します [!DNL GraphQL] カテゴリ階層の取得リクエスト [!UICONTROL product_count]:

<pre><code>
{
  categoryList(filters: { ids: { eq: "2" } }) {
    id
    name
    product_count
    level
    children {
      name
      product_count
      level
      children {
        name
        product_count
        level
        children {
          name
          product_count
          level
          children {
            name
            product_count
            level
          }
        }
      }
    }
  }
}
</code></pre>

<u>期待される結果</u>:

親カテゴリがアンカーされたカテゴリの場合、 [!UICONTROL product_count] は、すべてのレベルで子カテゴリの製品数の合計を表示する必要があります。

<u>実際の結果</u>:

親カテゴリがアンカーされたカテゴリの場合、製品はカテゴリ レベル 2 以下では 0 として表示されます。

<pre><code>
{
    "data": {
        "categoryList": [
            {
                "id": 2,
                "name": "Default Category",
                "product_count": 186,
                "level": 1,
                "children": [
                    {
                        "name": "What's New",
                        "product_count": 0,
                        "level": 2,
                        "children": []
                    },
                    {
                        "name": "Women",
                        "product_count": 0,
                        "level": 2,
                        "children": [
                            {
                                "name": "Tops",
                                "product_count": 0,
                                "level": 3,
                                "children": []
                            },
                            {
                                "name": "Bottoms",
                                "product_count": 0,
                                "level": 3,
                                "children": []
                            }
                        ]
                    },
                    ...
                ]
            }
        ]
    }
}
</code></pre>

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
