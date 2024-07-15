---
title: 「ACSD-51890:[!UICONTROL Submit review] ボタンを複数回クリックできる」
description: ACSD-51890 パッチを適用すると、検証を行わずに「[!UICONTROL Submit Review]」ボタンを複数回クリックできるAdobe Commerceの問題  [!DNL Google reCAPTCHA v3]  修正できます。
feature: Products
role: Admin
exl-id: f6369a24-24bd-4e5e-a870-a13f507ada94
source-git-commit: 7dbf9a796fe2026b0657b719d10e5bb21b964fb6
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# ACSD-51890：検証 **[!UICONTROL Submit Review]** なくてもボタンを複数回クリック **[!DNL Google reCAPTCHA v3]** きます

>[!NOTE]
>
>このパッチは [ACSD-55112](/help/support-tools/patches-available-in-qpt-tool/v1-1-42/acsd-55112-submit-review-button-can-be-clicked-multiple-times.md) に置き換えられます。

ACSD-51890 パッチは、検証を行わずに **[!UICONTROL Submit Review]** ボタンを複数回クリックできる問題 **[!DNL Google reCAPTCHA v3]** 修正しています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.35 がインストールされている場合に使用できます。 パッチ ID は ACSD-51890 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「**[!UICONTROL Submit Review]**」ボタンは、**[!DNL Google reCAPTCHA v3]** の検証を行わずに複数回クリックできます。

<u> 再現手順 </u>:

1. 製品レビュー用に **[!DNL Google reCAPTCHA v3]** を有効にします。
1. 製品ページを開き、「**[!UICONTROL Review]**」セクションに移動し、[!DNL reCAPTCHA] が表示されていることを確認します。
1. レビューフォームに入力し、「**[!UICONTROL Submit Review]**」ボタンをできるだけ早く複数回クリックします。
1. 管理者から「**[!UICONTROL Review]**」セクションを開きます。

<u> 期待される結果 </u>

重複するレビューは作成されません。

<u> 実績 </u>

重複するレビューが作成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>)」を参照してください。
