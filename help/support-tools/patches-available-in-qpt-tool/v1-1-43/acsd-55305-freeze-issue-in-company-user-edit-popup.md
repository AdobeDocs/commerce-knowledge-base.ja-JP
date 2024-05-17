---
title: 'ACSD-55305：での会社ユーザーの編集中にポップアップがフリーズする [!UICONTROL My Account]'
description: Adobe Commerceの問題を修正するために ACSD-55305 パッチを適用してください。この問題の場所は次のとおりです。 [!UICONTROL Edit Company User] のポップアップ [!UICONTROL My Account] &gt; [!UICONTROL Company Structure] 画面にローダーが表示されると、ページがフリーズする。
feature: Companies, B2B
role: Admin, Developer
exl-id: be2bfe08-d05e-485d-84c3-2ff14e1a8654
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# ACSD-55305：での会社ユーザーの編集中にポップアップがフリーズする [!UICONTROL My Account]

ACSD-55305 パッチは、次の問題を修正します。  [!UICONTROL Edit Company User] のポップアップ [!UICONTROL My Account]> [!UICONTROL Company Structure] 画面にローダーが表示されると、ページがフリーズする。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされています。 パッチ ID は ACSD-55305 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

を使用しようとすると、エラーが発生する *[!UICONTROL Edit Company User]* のポップアップ *[!UICONTROL My Account]* > *[!UICONTROL Company Structure]* ページは、画面に表示されたローダーでフリーズします。

<u>再現手順</u>:

1. B2B 会社を作成します。
1. 顧客用に複数選択属性を作成します。
1. 会社管理者の新しく作成した属性に値を割り当てます。
1. 会社管理者としてログインします。
1. に移動します [!UICONTROL account dashboard] に移動します。 **[!UICONTROL Company Structure]**.
1. ユーザーを選択します。
1. クリックする **[!UICONTROL Edit Selected]**.

<u>期待される結果</u>:

フォームのポップアップが正確に表示され、会社情報を編集するオプションが表示されます。

<u>実際の結果</u>:

フォームのポップアップが表示され、編集することはできません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
