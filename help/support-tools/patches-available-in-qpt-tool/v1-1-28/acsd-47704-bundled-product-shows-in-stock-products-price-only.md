---
title: 「ACSD-47704：バンドル製品は、在庫製品のみの価格を示します」
description: ACSD-47704 パッチを適用すると、バンドルされた製品に在庫製品のみの価格が表示されるAdobe Commerceの問題が修正されます。
exl-id: 91fbeaf7-4bc2-49b1-a561-c3e63f193eaa
feature: Admin Workspace, Customer Service, Orders, Products
role: Admin
source-git-commit: 3eeb86c2644f8a04ddcf5e205bc400d2ca9969af
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# ACSD-47704: バンドル製品は、在庫製品のみの価格を示します

ACSD-47704 パッチは、顧客セグメント価格が顧客グループ間で誤ってキャッシュされる問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされている場合に使用できます。 パッチ ID は ACSD-47704 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

動的価格設定が有効になっているバンドル製品の価格は、在庫品目のみが含まれているため、正しくありません。

<u> 再現手順 </u>:

1. Commerce管理パネルに移動します。
1. **[!UICONTROL CATALOG]**/**[!UICONTROL Products]**/**[!UICONTROL Add Product]**/**[!UICONTROL Bundle Product]** に移動します。
1. **[UICONROL Dynamic Price]** を **[!UICONTROL Yes]** に設定します。
1. バンドル項目：
   * **[!UICONTROL Ship bundle items]** を **[!UICONTROL Together]** に設定
   * Select **[!UICONTROL Add Option]**
      * **[!UICONTROL Title]** = o1
      * **[!UICONTROL Input type]** = **[!UICONTROL Dropdown]**
      * 必須チェックボックスをマーク
      * 在庫がある単純な製品（Jourst Duffle Bag SKU 24-MB01 など）を追加します。 製品を追加する前に、その価格をメモしてください – 34 ドル
   * 既定の数量：1
   * Select **[!UICONTROL Add Option]**
      * **[!UICONTROL Option Title]** = o2
      * **[!UICONTROL Input type]** = **[!UICONTROL Dropdown]**
      * 必須チェックボックスをマーク
      * 前の手順で追加した製品とは異なる、在庫がある単純な製品を追加します。例えば、- Steve Shoulder Pack 24-MB04。 製品を追加する前に、その価格をメモしてください – 32 ドル
      * 既定の数量：1
1. 製品を保存します。
1. ストアフロントに移動し、前の手順で作成した製品を見つけます。 その価格を書き留めます – 66 ドル
（66 = 32 + 34）。
現在、バンドル製品の価格は、そのオプションの価格の合計に等しい。
1. Commerce管理パネルに移動します。 **[!UICONTROL CATALOG]**/**[!UICONTROL Products]** に移動します。
1. 先に、バンドル製品にオプションとして割り当てられたシンプルな製品の 1 つを見つけます。
SKU 24-MB01、価格$34。
1. その量を 0 に変更します。
1. 商品を保存します。
1. ストアフロントに移動し、前の手順で作成したバンドル製品を見つけます。 その価格を書き留めます – 32 ドル。 以前は 66 ドルと設定されていましたが、これは SKU 24-MB01 の 34 ドルと SKU 24-MB04 の 32 ドルの合計です。 これで製品 24-MB01 が在庫切れになったので、バンドル価格は 32 ドルと表示されます。 これは、在庫オプションである他の製品の価格です。

<u> 期待される結果 </u>:

動的価格設定が有効になっているバンドル製品の価格は、オプションが在庫にあるか在庫切れかに関係なく、一貫して計算されます。

<u> 実際の結果 </u>:

動的価格設定が有効になっているバンドル製品の価格の計算が誤っています。 在庫があるオプションのみを考慮しているので、いずれかのオプションが在庫切れの場合は、実際のオプションよりも金額が低く表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
