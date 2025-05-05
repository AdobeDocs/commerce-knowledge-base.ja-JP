---
title: 「ACSD-46683：送料に「未計算」と表示される」
description: ACSD-46683 パッチを適用すると、送料に「未計算」と表示されるAdobe Commerceの問題が修正されます。
exl-id: 77986612-87b7-4f50-afaf-1cfe9a4feb6f
feature: Marketing Tools, Orders, Shipping/Delivery
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# ACSD-46683：送料が表示されます *まだ計算されていません*

ACSD-46683 パッチは、配送価格に *まだ計算されていません* と表示される問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされている場合に使用できます。 パッチ ID は ACSD-46683 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

配送料は *まだ計算されていません* と表示されます。

<u> 前提条件 </u>:

Adobe Commerce Inventory management（MSI）モジュールがインストールされている。

<u> 再現手順 </u>:

1. 簡単な製品を作成し、その価格を *$34* に設定します。
1. 送料無料の配信方法を設定します。
1. 1 つ以上の配信方法を設定します。
1. **[!UICONTROL Marketing]**/**[!UICONTROL Cart Price Rules]** に移動して、新しいルールを作成します。
   * 名前= *75more*
   * クーポン =なし
   * 優先度= 1
   * 条件：小計が *$75* 以上
   * アクション：
      * 出荷金額に適用= Yes
      * 後続のルールを破棄= No
      * 送料無料=商品が一致する配送の場合
1. 別の買い物かご価格ルールを作成します。
   * 名前= *35off*
   * 優先度= 0
   * クーポン =特定のクーポン
   * クーポンコード = 35off
   * アクション：
      * 適用=製品価格割引率
      * 割引額= 35
      * 出荷金額に適用= No
      * 後続のルールを破棄= Yes
      * 送料無料= No
1. ストアフロントを開き、買い物かごに 3 つの製品を追加して、小計が 75 ドルを超えるようにします。
1. ゲストとしてチェックアウトに進みます。
1. 配送手順で、**$0 – 送料無料を選択し** 支払い手順に進みます。
1. 支払い手順の [!UICONTROL Order Summary] を確認してください。 それは *[!UICONTROL $0 - Free Shipping - Free]* を示します。
1. クーポンコード *35off* を適用すると、小計が更新され、75 ドル未満になります。
1. 支払い手順で [!UICONTROL Order Summary] を確認します。

<u> 期待される結果 </u>:

次のメッセージが表示されます。*選択された発送方法は使用できません。 この注文に対して別の配送方法を選択してください。*

<u> 実際の結果 </u>:

出荷価格は *まだ計算されていません* と表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
