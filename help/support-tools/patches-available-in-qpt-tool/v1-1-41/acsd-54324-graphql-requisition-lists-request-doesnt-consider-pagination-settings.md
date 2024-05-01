---
title: 「ACSD-54324:GraphQL requisition_lists リクエストでページネーションの設定が考慮されない」
description: ACSD-54324 パッチを適用すると、Adobe Commerceの「requisition_lists」リクエストでページネーションの設定が考慮されず、すべての結果が返されるGraphQLの問題を修正できます。
feature: B2B, Customers, GraphQL
role: Admin, Developer
exl-id: 85297eae-bedf-4624-9758-0b68452d131b
source-git-commit: b5894687704594a4e751c230246bdf167b1b6402
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# ACSD-54324:GraphQL `requisition_lists` リクエストがページネーションの設定を考慮しない

ACSD-54324 パッチにより、GraphQLが原因で発生していた問題が修正されました `requisition_lists` リクエストがページネーションの設定を考慮せず、すべての結果を返します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.41 がインストールされています。 パッチ ID は ACSD-54324 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQL `requisition_lists` リクエストがページネーションの設定を考慮せず、すべての結果を返します。

<u>再現手順</u>:

1. 管理者にログインし、に移動します。 **[!UICONTROL Admin]** > **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL General]** > **[!UICONTROL B2B Features]**.

   * を設定 *[!UICONTROL Enable Requisition List]* 対象： *はい*.

1. フロントエンドにログインし、に移動します **[!UICONTROL My Requisition Lists]** トップメニューから、または **[!UICONTROL My Account]**&#x200B;を選択し、複数の購買依頼を作成します（例：7）。
1. カスタマートークンを生成したら、以下のGraphQLを実行します `requisition_lists` 顧客のをクエリします。

   * ページ・サイズが、作成した購買依頼リストの合計数より少ないことを確認します（例：4）

   ```
   {
   customer {
   requisition_lists(pageSize: 4, currentPage: 1) {
   items
   
   { uid name description updated_at items_count }
   total_count
   }
   }
   }
   ```

1. の値 `total_count` フィールドには 7 と表示されますが、4 と表示されます。

   また、項目数が同じである必要がある場合は、7 と表示されます。 *ページサイズ*.

<u>期待される結果</u>:

* としてリストされた数 *ページサイズ* は次の場所で返されます `total_count` レコードの合計数ではありません。
* 項目の数は *ページサイズ*.

<u>実際の結果</u>:

レコードの合計数は、次の場所で返されます `total_count`次の場合でも *ページサイズ* が記載されています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
