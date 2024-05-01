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

ACSD-46683 パッチは、配送価格が表示される問題を修正します *まだ計算されていません*. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は ACSD-46683 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

送料が表示されます *まだ計算されていません*.

<u>前提条件</u>:

Adobe Commerce Inventory management（MSI）モジュールがインストールされている。

<u>再現手順</u>:

1. シンプルな製品を作成し、その価格をに設定 *$34*.
1. 送料無料の配信方法を設定します。
1. 1 つ以上の配信方法を設定します。
1. に移動 **[!UICONTROL Marketing]** > **[!UICONTROL Cart Price Rules]** 新しいルールを作成します。
   * 名前= *75 その他*
   * クーポン =なし
   * 優先度= 1
   * 条件：小計が以上 *$75*
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
1. 出荷手順で、次の項目を選択します **$0 – 送料無料** そして支払いステップに進みます。
1. を確認します [!UICONTROL Order Summary] 支払い手順で。 それが示すのは *[!UICONTROL $0 - Free Shipping - Free]*.
1. クーポンコードの適用 *35off*&#x200B;小計が更新され、75 ドル未満になります。
1. チェック [!UICONTROL Order Summary] 支払い手順で。

<u>期待される結果</u>:

次のメッセージが表示されます。 *選択した配送方法は利用できません。 この注文には別の配送方法を選択してください。*

<u>実際の結果</u>:

配送料が表示されます *まだ計算されていません*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
