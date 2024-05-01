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

ACSD-56886 パッチは、子製品が無効になっている場合に設定可能な製品が在庫切れになる問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされています。 パッチ ID は ACSD-56886 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

子製品が無効になると、設定可能な製品は在庫切れになります。

<u>再現手順</u>:

1. 管理者としてログインします。
1. にインデクサーをすべて設定 **[!UICONTROL Update By Schedule]** モード。
1. 次の設定可能な製品を作成します。

   * 名前= *テスト設定可能 1*
   * 属性= *色*
   * 値= *赤* および *黒*
   * 価格： **赤**  子製品= *100 ドル*;
   * 「黒」の子製品の価格= *200 ドル*.

1. 設定可能な製品に対して、次のスケジュール済み更新を作成します。

   * 開始日= *3* 今から分です。
   * 終了日= *5* 分後開始日。
   * 製品名= *テスト設定可能 1 を編集しました*.
   * を無効にする **赤** 子製品： **設定可能** セクション。

1. 開始日を待ちます。
1. ストアフロントで設定可能な製品詳細を開きます。

<u>期待される結果</u>:

設定可能な製品は次のように表示されます **在庫あり** （を使用） **200 まで** ラベル。

<u>実際の結果</u>:

設定可能な製品は次のように表示されます **在庫切れ**.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
