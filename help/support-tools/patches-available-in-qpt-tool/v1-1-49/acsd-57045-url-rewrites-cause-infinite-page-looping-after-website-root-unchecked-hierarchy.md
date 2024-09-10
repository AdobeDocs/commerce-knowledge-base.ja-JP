---
title: 「ACSD-57045:URL の書き換えを使用すると、[!UICONTROL Hierarchy] からオフにした後に無限ページループ [!UICONTROL Website Root] 発生する」
description: ACSD-57045 パッチを適用して、URL の書き換えによって [!UICONTROL Hierarchy] からオフにした後に無限ページループが発生す [!UICONTROL Website Root]Adobe Commerceの問題を修正してください。
feature: CMS
role: Admin, Developer
source-git-commit: df6cfc392f6afa4639a1ab9da52a85b8b15878d2
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# ACSD-57045:URL の書き換えを [!UICONTROL Hierarchy] からオフにすると、無限ページのループ [!UICONTROL Website Root] 発生する

ACSD-57045 パッチでは、**[!UICONTROL Website Root]** をオフにした後に URL の書き換えによって無限ページループが発生する問題が修正されて **[!UICONTROL Hierarchy]** ます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.49 がインストールされている場合に使用できます。 パッチ ID は ACSD-57045 です。 この問題はAdobe Commerce 2.5.0 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p7

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

URL の書き換えは、**[!UICONTROL Website Root]** が **[!UICONTROL Hierarchy]** から選択解除された後、無限ページループを引き起こします。

<u> 再現手順 </u>:

1. *Test-Parent* という名前のCMS ページを作成します。
1. *Test-Child* という名前のページを作成し、「**[!UICONTROL Hierarchy]**」セクションで「**[!UICONTROL Website Root]**」 > 「**[!UICONTROL Parent]**」を選択して保存します。
1. **[!UICONTROL Marketing]**/**[!UICONTROL URL Rewrites]** に移動します。
1. 次の 2 つの新しい書き換えがあることに注意してください。
   * *cms/page/view/page_id/ID_NUMBER_FOR_PAGE* を指す *Test-Parent* へのリクエストパス
   * *cms/page/view/page_id/ID_NUMBER_FOR_PAGE* を指す *Test-Child* へのリクエストパス
1. ストアフロントにアクセスし、URL に *test-child* を追加します。 子ページが表示されます。
1. 同じことを行い、URL に *test-parent/test-child/* を追加して、同じページを表示します。
1. **[!UICONTROL Marketing]**/**[!UICONTROL URL Rewrites]** に移動し、「**[!UICONTROL Add URL Rewrite]**」を選択します。 次の設定を選択します。
   * タイプ：*カスタム*
   * リクエストパス：*test-parent/test-child*
   * ターゲットパス：*test-child*
   * リダイレクトタイプ：*パーマネント（301）*
1. *test-parent/test-child* パスにアクセスすると、*test-child* にリダイレクトされます。
1. 子ページを編集します（**[!UICONTROL Content]**/**[!UICONTROL Elements]**/**[!UICONTROL Pages]**/子を選択して **[!UICONTROL Edit]** を選択）。
1. 「**[!UICONTROL Hierarchy]**」セクションで、*Test-Parent* を選択したまま、選択を解除して保存 **[!UICONTROL Website Root]** ます。
1. **[!UICONTROL Marketing]**/**[!UICONTROL URL Rewrites]** に移動して、*cms/page/view/page_id* リダイレクトへの元の *test-child* が見つからず、その時点で、*test-child* を *test-parent/test-child* に指すパスに置き換えられていることに注意してください。
1. ストアフロントにアクセスして、*テストチャイルド* ページにアクセスしてみてください。

<u> 期待される結果 </u>:

*Test-Child* ページが開きます。

<u> 実際の結果 </u>:

*Test-Child* ページが開かれません。 ブラウザーは、*test-parent/test-child* ページを無限ループで開こうとします。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
