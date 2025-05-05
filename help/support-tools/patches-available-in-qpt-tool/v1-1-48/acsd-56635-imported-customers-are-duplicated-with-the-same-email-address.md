---
title: 「ACSD-56635：アカウント共有がに設定されている場合、読み込まれた顧客は重複します  [!DNL Global]」
description: ACSD-56635 パッチを適用すると、読み込みをアカウント共有を  [!DNL Global] に設定して使用した場合、読み込んだお客様が同じメールアドレスで重複するAdobe Commerceの問題が修正されます。
feature: Customers, Attributes
role: Admin, Developer
exl-id: abd542a1-6764-4385-97a6-b46015363b42
source-git-commit: 880fc679afc853b514fddda56e570fe1a279a3d9
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# ACSD-56635：アカウント共有が [!DNL Global] に設定されている場合、インポートされた顧客は同じメールアドレスで重複します

ACSD-56635 パッチは、アカウント共有を [!DNL Global] に設定した状態で読み込みを使用すると、読み込まれた顧客が同じメールアドレスで重複する問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされている場合に使用できます。 パッチ ID は ACSD-56635 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

アカウント共有が [!DNL Global] に設定されている場合、読み込まれた顧客は同じメールアドレスで複製されます。

<u> 再現手順 </u>:

1. Adobe Commerce（2.4-develop b2b） **[!UICONTROL Admin]** で、**[!UICONTROL Stores]**/**[!UICONTROL Settings]**/**[!UICONTROL Configuration]**/**[!UICONTROL Customers]**/**[!UICONTROL Customer Configuration]**/**[!UICONTROL Account Sharing Options]** にアクセスします。
1. *[!UICONTROL Share Customer Accounts]* 設定を *[!DNL Global]* に設定します。
1. 複数の web サイトとストアを作成します。

   * ws1 > s11, s12 > sw111, sw122
   * ws2 > s21, s22 > sw211, sw212

1. *メイン web サイト* の下に、管理者から、<adb@yormail.com> として使用するメールアドレスで新しい顧客を作成します。
1. **[!UICONTROL Admin]** の下で、**[!UICONTROL System]**/**[!UICONTROL Import]** に移動します。
1. *[!UICONTROL Customers Main File]* として **[!UICONTROL Customer Entity Type]** を選択します。
1. 別の web サイトの <adb@yormail.com> と同じメールアドレス（例：ws1）を使用します。 以下に示すサンプル CSV ファイル customer.csv を参照してください。
1. 読み込みを完了して、同じメールアドレスを持つ *ws1* web サイトで作成された新しいユーザーを確認します。

customer.csv コンテンツ：

```
email,_website,_store,confirmation,created_at,created_in,disable_auto_group_change,dob,firstname,gender,group_id,lastname,middlename,password_hash,prefix,rp_token,rp_token_created_at,store_id,suffix,taxvat,updated_at,website_id,password
adb@yopmail.com,ws1,sv111,,09/01/24 12:49,Default Store View,0,,newjon,,1,newDoe,,d708be3fe0fe0120840e8b13c8faae97424252c6374227ff59c05814f1aecd79:mgLqkqgTwLPLlCljzvF8hp67fNOOvOZb:1,,07e71459c137f4da15292134ff459cba,30/10/15 12:49,1,,,09/01/24 12:49,1,
```

<u> 期待される結果 </u>:

同じメールアドレスを持つ、読み込まれた顧客は、複製されずに更新されます。

<u> 実際の結果 </u>:

顧客インポートを使用すると、重複した顧客は同じメールアドレスで作成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
