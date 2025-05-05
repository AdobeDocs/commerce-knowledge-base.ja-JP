---
title: 「ACSD-53643：発注書を送信する際、注文の合計が間違っている」
description: 無効な商品や在庫切れの商品を使用して注文を行った際に、注文の合計が正しくないAdobe Commerceの問題を修正するために、ACSD-53643 パッチを適用してください。
feature: B2B
role: Admin, Developer
exl-id: 9843e07a-8a17-401e-98bc-559df5148d34
source-git-commit: 2356ac10b05ae9f38e5c0ca90d9156b0fc405718
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# ACSD-53643：発注書を発注する際に、注文の合計が間違って表示される

ACSD-53643 パッチは、無効な製品または在庫切れの製品を使用して注文を行った際に、注文の合計が正しくない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.41 がインストールされている場合に使用できます。 パッチ ID は ACSD-53643 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

無効な製品または在庫切れの製品を使用して発注書を送信すると、注文合計が正しく表示されません。

<u> 再現手順 </u>:

1. *[!UICONTROL B2B]* と *[!UICONTROL Inventory]* をインストールします。
1. **[!UICONTROL Admin]**/**[!UICONTROL Store]**/**[!UICONTROL Configuration]**/**[!UICONTROL B2B]** に移動して、**[!UICONTROL Company]** = *はい* および **[!UICONTROL Purchase Order]** = *はい* を設定します。
1. 設定キャッシュをクリアします。
1. 新しい会社を作成してアクティブにし、会社の *[!UICONTROL Purchase order]* を有効にします。
1. 会社の新規ユーザーを作成します。
1. 会社管理者によって *1 米ドル* を超えるすべての注文を承認する *承認ルール* を作成します。
1. 追加のソースを作成します
1. 新しい会社ユーザーとしてログインします。
1. 2 つの製品を買い物かごに追加し、購入オーダーを行います。
1. 2 番目の製品を無効にします。
1. 会社管理者としてログインします。
1. 発注書を開き、発注書に両方の商品が含まれ、合計が両方の商品であることを確認します。
1. 発注書を承認します。
1. 注文します。
1. 注文の詳細を開きます。

<u> 期待される結果 </u>:

* 注文内の 1 つの製品が *無効* または *在庫切れ* の場合でも、注文できません。
* ボタン *[!UICONTROL Place Order]* 非表示です。

<u> 実際の結果 </u>:

注文には最初のアクティブな商品のみが含まれていますが、注文の合計は両方の商品について計算されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
