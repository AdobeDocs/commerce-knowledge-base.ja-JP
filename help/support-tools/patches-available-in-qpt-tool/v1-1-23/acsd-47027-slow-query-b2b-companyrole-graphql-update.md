---
title: 'ACSD-47027：低速クエリ B2B [!UICONTROL CompanyRole] [!DNL GraphQL] 更新'
description: ACSD-47027 パッチを適用して、クエリ B2B が遅いAdobe Commerceの問題を修正してください [!UICONTROL CompanyRole] [!DNL GraphQL] 更新。
exl-id: 478ae16b-7722-4469-8f8a-a38820e61ae4
feature: B2B, Companies, GraphQL, Roles/Permissions
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# ACSD-47027：低速クエリ B2B [!UICONTROL CompanyRole] [!DNL GraphQL] 更新

ACSD-47027 パッチは、低速のクエリ B2B が発生する問題を解決します [!UICONTROL CompanyRole] [!DNL GraphQL] 更新が期待どおりに動作しません。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.23 がインストールされています。 パッチ ID は ACSD-47027 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

低速クエリ B2B [!UICONTROL CompanyRole] [!DNL GraphQL] 更新が期待どおりに動作しません。

<u>前提条件</u>:

B2B モジュールをインストールします。

<u>再現手順</u>:

1. Adobe Commerce Admin で、に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configurations]** > **[!UICONTROL B2B Features]** およびを設定 **[!UICONTROL Enable Company]** 対象： _はい_.
1. フロントエンドに移動し、会社を作成します。
1. 会社ユーザーとしてログインしたら、次の場所に移動します **[!UICONTROL My Account]** > **[!UICONTROL Roles and Permissions]** 新しい役割を追加します。
1. Enable （有効） [!UICONTROL dev] を使用したクエリログ `bin/magento dev:que:enab`.
1. 次を送信します [!DNL GraphQL] リクエスト （id は [!UICONTROL base64] エンコードされた役割 id）:

   <pre><code>
   mutation {
   updateCompanyRole(
      input: {
         id: "Mg=="
         permissions: [
         "Magento_Company::view"
         "Magento_Company::view_account"
         "Magento_Company::user_management"
         "Magento_Company::roles_view"
        ]
      }
    ) {
      role {
         id

         name

         permissions {
         id

         text

         children {
            id

            text

            children {
               id

               text
             }
           }
         }
       }
     }
   }
   </code></pre>

1. クエリログを確認します。
1. 上記のクエリが実行されていることがわかります。 このクエリの実行場所 `app/code/Magento/CompanyGraphQl/Model/Company/Role/ValidateRole.php::validateResources`.

<u>期待される結果</u>:

この `app/code/Magento/CompanyGraphQl/Model/Company/Role/ValidateRole.php::validateResources` で利用可能なすべてのデータを読み込まないように最適化する必要があります。 **[!UICONTROL company_permissions]** DB テーブル。

<u>実際の結果</u>:

Adobe Commerceは、フィルターなしでクエリを実行します。 レコード数が多い場合、Adobe Commerceでのデータ収集の準備に多くの時間がかかります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。 

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
