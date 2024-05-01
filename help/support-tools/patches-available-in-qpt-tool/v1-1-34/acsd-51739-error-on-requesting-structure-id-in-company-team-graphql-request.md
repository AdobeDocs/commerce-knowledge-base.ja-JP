---
title: 「ACSD-51739:「CompanyTeam」GraphQL リクエストの「structure_id」をリクエスト中にエラーが発生しました」
description: ACSD-51739 パッチを適用すると、「CompanyTeam」GraphQL リクエストで「structure_id」がリクエストされた場合にエラーが返されるAdobe Commerceの問題を修正できます。
exl-id: 31c085e0-c8be-4709-9620-80ff360dca9a
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# ACSD-51739：要求時のエラー `structure_id` 。対象： `CompanyTeam` GraphQL リクエスト

ACSD-51739 パッチは、 `structure_id` 次でリクエストされた `CompanyTeam` GraphQL リクエスト。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.34 がインストールされています。 パッチ ID は ACSD-51739 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

エラーが返されるのは、 `structure_id` 次でリクエストされた `CompanyTeam` GraphQL リクエスト。

<u>再現手順</u>

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL General]** > **[!UICONTROL B2B Features]**、およびを設定 *[!UICONTROL Enable Company]* 対象： *はい*.
1. 会社を会社管理者ユーザーと共に作成します。
1. 顧客の新規作成（*customer1*）を選択し、（上記で作成した）会社をこの顧客に割り当てます。
1. フロントエンドで、会社の管理者ユーザーとしてログインします。
1. 会社チームを作成して割り当て *customer1* ドラッグ&amp;ドロップでチームに追加できます。
1. 次の会社 GraphQl クエリを実行します。これには、以下が含まれます `CompanyTeam` （を使用） `structure_id`:

   ```GraphQL
   query{
       company {
           id
           name
           structure {
               items {
               id
               parent_id
               entity {
                   __typename
                   ... on Customer {
                       firstname
                       lastname
                       email
                       structure_id
                   }
                   ... on CompanyTeam {
                       id
                       name
                       structure_id
                   }
               }
       }
   }
   }
   }
   ```

1. GraphQLの応答を確認します。

<u>期待される結果</u>:

エラーは返されず、リクエストされたすべてのデータがGraphQL応答に存在します。

<u>実際の結果</u>:

* 応答にが含まれる *内部サーバーエラー*.
* `var/log/exception.log` 含む：

  ```
  report.ERROR: Cannot return null for non-nullable field "CompanyTeam.structure_id"
  ```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
