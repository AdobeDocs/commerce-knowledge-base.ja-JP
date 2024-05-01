---
title: 「ACSD-52133：アップグレード後に顧客アカウントを保存できない」
description: ACSD-52133 パッチを適用すると、アップグレード後にカスタマーアカウントを保存できないAdobe Commerceの問題を修正できます。
feature: Customers, Upgrade
role: Admin
exl-id: 0db7c79e-10e1-4850-81b5-4812fb051941
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# ACSD-52133：アップグレード後に顧客アカウントを保存できない

ACSD-52133 パッチにより、アップグレード後にカスタマーアカウントを保存できない問題が修正されました。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-52133 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

アップグレード後に顧客アカウントを保存することはできません。

<u>再現手順</u>:

1. Adobe Commerce バージョン 2.4.4 をインストールします。
1. 顧客を作成します。
1. Adobe Commerceを、お客様が既に作成されている以前のバージョンの 2.4.4 から 2.4.6 にアップグレードします。
1. 次のように暗号化キーを設定します。 `env.php`:

   `d337b914e91ff703b1e94ba4156aadf0`

1. 以下の値を、以下に該当する顧客のデータベースに設定します。 `customer_entity` テーブル：

   ```
   -> rp_token as incr4869
   -> rp_token_created_at as "2021-04-29 20:06:14"
   ```

1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Customers]** > **[!UICONTROL All Customers]**.
1. 上記の値を更新した顧客を編集します。
1. クリックする **[!UICONTROL Save Customer]** または **[!UICONTROL Save and Continue Edit]**

<u>期待される結果</u>:

顧客はエラーなしで正常に保存されました。

<u>実際の結果</u>:

* 顧客レコードは保存されません。
* 管理者に次のエラーメッセージが表示されます。 *顧客の保存中にエラーが発生しました。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
