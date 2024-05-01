---
title: 「ACSD-51379：次を使用したページのテキストコンテンツの変更 [!DNL Page Builder] は保存されませんでした」
description: ACSD-51379 パッチを適用すると、を介してページのテキストコンテンツに変更が加えられるAdobe Commerceの問題を修正できます。 [!DNL Page Builder] は保存されません。
exl-id: e274ca03-b675-4ded-9820-1d60978685d0
feature: Page Builder, Page Content
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# ACSD-51379：を使用したページのテキストコンテンツの変更 [!DNL Page Builder] は保存されませんでした

ACSD-51379 パッチは、を介してページのテキストコンテンツに変更が加えられる問題を修正します [!DNL Page Builder] は保存されません。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.32 がインストールされています。 パッチ ID は ACSD-51379 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

を介してページのテキストコンテンツに加えられた変更 [!DNL Page Builder] は保存されません。

<u>再現手順</u>:

1. 管理者にログインします。
1. に移動 **[!UICONTROL Content]** > **[!UICONTROL Elements]** > **[!UICONTROL Pages]**.
1. 上に 1 つの行と 1 つのテキスト要素を持つテストページを作成します **[!UICONTROL Content]** タブ。
1. ページを保存し、に戻ります **[!UICONTROL Content]** タブ。
1. テキストを選択して変更することで、テキストを編集します。

   **注意：** この問題は、エディターをアクティブ化せずにテキストを選択および変更した場合にのみ再現できます。

1. 「」をクリックします **[!UICONTROL Save and Close]** テストページの「」ボタン。
1. テストページを再度開き、 **[!UICONTROL Content]** タブ。

<u>期待される結果</u>:

元のテキスト要素と複製されたテキスト要素に対して、新しいテキストが正常に保存されます。

<u>実際の結果</u>:

テキスト要素は正常に複製されましたが、新しいテキストは保存されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
