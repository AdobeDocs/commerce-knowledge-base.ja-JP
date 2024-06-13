---
title: 'ACSD-56635：アカウント共有がに設定されている場合、読み込まれた顧客は重複します [!DNL Global]'
description: ACSD-56635 パッチを適用すると、読み込みを使用しアカウント共有をに設定すると、読み込んだお客様が同じメールアドレスで重複するAdobe Commerceの問題が修正されます [!DNL Global].
feature: Customers, Attributes
role: Admin, Developer
exl-id: abd542a1-6764-4385-97a6-b46015363b42
source-git-commit: 880fc679afc853b514fddda56e570fe1a279a3d9
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# ACSD-56635：アカウント共有がに設定されている場合、インポートされた顧客は同じメールアドレスで重複します。 [!DNL Global]

ACSD-56635 パッチは、アカウント共有をに設定して読み込みを使用すると、読み込まれた顧客が同じメールアドレスで重複する問題を修正します [!DNL Global]. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされています。 パッチ ID は ACSD-56635 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

アカウント共有がに設定されている場合、読み込まれた顧客は同じメールアドレスで複製されます。 [!DNL Global].

<u>再現手順</u>:

1. Adobe Commerceの下（2.4 – 開発 b2b） **[!UICONTROL Admin]**、アクセス **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Customers]** > **[!UICONTROL Customer Configuration]** > **[!UICONTROL Account Sharing Options]**.
1. を *[!UICONTROL Share Customer Accounts]* をに設定しています *[!DNL Global]*.
1. 複数の web サイトとストアを作成します。

   * ws1 > s11, s12 > sw111, sw122
   * ws2 > s21, s22 > sw211, sw212

1. 「」の下に新しい顧客を作成します *メイン web サイト* 管理者から（電子メールアドレスはとして使用） <adb@yormail.com>.
1. 次の下 **[!UICONTROL Admin]**&#x200B;に移動します。 **[!UICONTROL System]** > **[!UICONTROL Import]**.
1. を選択 **[!UICONTROL Customer Entity Type]** as *[!UICONTROL Customers Main File]*.
1. 同じメールアドレスを使用 <adb@yormail.com> 別の web サイト（例：ws1） 以下に示すサンプル CSV ファイル customer.csv を参照してください。
1. 読み込みを完了して、で作成された新しいユーザーを確認します。 *ws1* 同じメールアドレスを持つ web サイト。

customer.csv コンテンツ：

```
email,_website,_store,confirmation,created_at,created_in,disable_auto_group_change,dob,firstname,gender,group_id,lastname,middlename,password_hash,prefix,rp_token,rp_token_created_at,store_id,suffix,taxvat,updated_at,website_id,password
adb@yopmail.com,ws1,sv111,,09/01/24 12:49,Default Store View,0,,newjon,,1,newDoe,,d708be3fe0fe0120840e8b13c8faae97424252c6374227ff59c05814f1aecd79:mgLqkqgTwLPLlCljzvF8hp67fNOOvOZb:1,,07e71459c137f4da15292134ff459cba,30/10/15 12:49,1,,,09/01/24 12:49,1,
```

<u>期待される結果</u>:

同じメールアドレスを持つ、読み込まれた顧客は、複製されずに更新されます。

<u>実際の結果</u>:

顧客インポートを使用すると、重複した顧客は同じメールアドレスで作成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
