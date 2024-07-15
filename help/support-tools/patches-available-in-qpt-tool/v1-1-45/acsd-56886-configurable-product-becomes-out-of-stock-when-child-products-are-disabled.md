---
title: 「ACSD-56886：子製品が無効になると、設定可能な製品が在庫切れになる」
description: ACSD-56886 パッチを適用して、商品が無効になると設定可能な商品が在庫切れになるAdobe Commerceの問題を修正してください。
feature: Products
role: Admin, Developer
exl-id: 809b9829-283f-4e3c-bf27-1944057f944f
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# ACSD-56886：子製品が無効になると、設定可能な製品が在庫切れになります

ACSD-56886 パッチは、子製品が無効になっている場合に設定可能な製品が在庫切れになる問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされている場合に使用できます。 パッチ ID は ACSD-56886 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

子製品が無効になると、設定可能な製品は在庫切れになります。

<u> 再現手順 </u>:

1. 管理者としてログインします。
1. すべてのインデクサーを **[!UICONTROL Update By Schedule]** モードで設定します。
1. 次の設定可能な製品を作成します。

   * 名前= *テスト設定可能 1*
   * Attribute = *color*
   * 値= *red* および *black*
   * **赤** 子製品の価格= *$100*;
   * 「黒」の子製品の価格= *$200*。

1. 設定可能な製品に対して、次のスケジュール済み更新を作成します。

   * 開始日=今から *3* 分後。
   * 終了日=開始日から *5* 分後。
   * 製品名= *テスト設定可能 1 を編集*。
   * 「**設定可能** セクションの **red** 子製品を無効にします。

1. 開始日を待ちます。
1. ストアフロントで設定可能な製品詳細を開きます。

<u> 期待される結果 </u>:

設定可能な製品は、**在庫中** と **200 以下** のラベルで表示されます。

<u> 実際の結果 </u>:

設定可能な商品が「在庫切れ **と表示さ** ます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
