---
title: 「ACSD-58008：終了日を*空*として編集すると、スケジュールの更新が表示されない」
description: ACSD-58008 パッチを適用して、終了日を*空*に変更するとスケジュールの更新が消えるAdobe Commerceの問題を修正してください。
feature: Staging, Page Content
role: Admin, Developer
exl-id: bfa590b8-377b-49dd-9aff-f89b8fd815c4
source-git-commit: d7ace1f20defb01105d4a241f971b06fca052215
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# ACSD-58008：終了日を *空* として編集すると、スケジュールの更新が表示されなくなります

ACSD-58008 パッチでは、終了日を *空* として編集すると、スケジュールの更新が消える問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされている場合に使用できます。 パッチ ID は ACSD-58008 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

終了日を *空* として編集すると、スケジュールの更新が表示されなくなります

<u> 再現手順 </u>:

1. [!UICONTROL Admin] としてログインします。
1. **[!UICONTROL Content]**/**[!UICONTROL Elements]**/**[!UICONTROL Pages]** に移動し、ページを作成します。
1. 作成したページを選択し、「**[!UICONTROL Schedule New Update]**」をクリックします。 *（ページの右上隅に移動します）*。
1. 4 つの更新を作成します。 *（例：* 2 *分）増分として*。
1. *update 2* を更新し、時間を最後の *update 4* より前の時間に変更します。
1. 行われた更新を保存します。

<u> 期待される結果 </u>:

スケジュールの更新では、*update 3* が表示されます。

<u> 実際の結果 </u>:

スケジュールの更新で *更新 3* が表示されない。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
