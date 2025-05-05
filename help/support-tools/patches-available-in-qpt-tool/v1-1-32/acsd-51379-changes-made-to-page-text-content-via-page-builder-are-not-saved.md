---
title: '「ACSD-51379: [!DNL Page Builder]  を使用したページのテキストコンテンツの変更は保存されません」'
description: ACSD-51379 パッチを適用すると、 [!DNL Page Builder]  を介してページのテキストコンテンツに加えられた変更が保存されないAdobe Commerceの問題を修正できます。
exl-id: e274ca03-b675-4ded-9820-1d60978685d0
feature: Page Builder, Page Content
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# ACSD-51379:[!DNL Page Builder] を使用したページのテキストコンテンツへの変更は保存されません

ACSD-51379 パッチにより、[!DNL Page Builder] を使用してページのテキストコンテンツに加えられた変更が保存されない問題が修正されました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.32 がインストールされている場合に使用できます。 パッチ ID は ACSD-51379 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 - 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL Page Builder] を使用してページのテキストコンテンツに加えられた変更は保存されません。

<u> 再現手順 </u>:

1. 管理者にログインします。
1. **[!UICONTROL Content]**/**[!UICONTROL Elements]**/**[!UICONTROL Pages]** に移動します。
1. 「**[!UICONTROL Content]**」タブに、1 つの行と 1 つのテキスト要素を持つテストページを作成します。
1. ページを保存し、「**[!UICONTROL Content]**」タブに戻ります。
1. テキストを選択して変更することで、テキストを編集します。

   **メモ：** この問題は、エディターをアクティブ化せずにテキストを選択および変更した場合にのみ、再現できます。

1. テストページで「**[!UICONTROL Save and Close]**」ボタンをクリックします。
1. テストページを再度開き、「**[!UICONTROL Content]**」タブを確認します。

<u> 期待される結果 </u>:

元のテキスト要素と複製されたテキスト要素に対して、新しいテキストが正常に保存されます。

<u> 実際の結果 </u>:

テキスト要素は正常に複製されましたが、新しいテキストは保存されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
