---
title: 「MDVA-30837：送料無料の最小注文金額」
description: MDVA-30837 パッチは、送料計算の構成オプションを追加します。これにより、ユーザーは小計（または総計）に基づいて送料無料を受け取るための最小注文額を構成できます。 これにより、税金および配送方法をローカルでカスタマイズできます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 64716d08-4ce0-40d5-aeb7-242e2aa85bb0
feature: Marketing Tools, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---

# MDVA-30837：送料無料の最小注文金額

MDVA-30837 パッチは、送料計算の構成オプションを追加します。これにより、ユーザーは小計（または総計）に基づいて送料無料を受け取るための最小注文額を構成できます。 これにより、税金および配送方法をローカルでカスタマイズできます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.1 - 2.3.4-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

パッチ MDVA-30837 は、設定を追加して、 **最小注文金額** 小計（または総計）に基づいて送料無料を取得するための設定：

* **金額に税を含める**: *はい/いいえ* （送料無料の方法の設定で確認できます）。
   * 条件 **金額に税を含める** はに設定されています。 *はい*&#x200B;最小注文額は、小計+税 – 割引として計算されます。
   * 条件 **金額に税を含める** はに設定されています。 *不可*&#x200B;の場合、最小注文額は小計 – 割引として計算されます。

<u>再現手順</u>:

1. に移動 **ストア** > 設定 > **設定** > **売上** > **税** を設定して、以下を行います。

   * 基づく税金計算 *発送先住所*
   * 国境を越えた貿易を実現： *不可*
   * カタログに価格を表示： *税別*
   * 配送料の表示： *税別*
   * 表示価格： *税別*
   * 小計を表示： *税別*
   * 配送料の表示： *税別*
   * ギフト折り返し価格の表示： *税別*
   * 印刷されたカードの価格を表示する： *税別*
   * 受注合計に税金を含む： *はい*
   * 全税概要の表示： *はい*

1. に移動 **売上** > **発送設定** > **送料無料** およびを設定 **最小注文金額** = *30*.
1. に移動 **Marketing** > プロモーション > **買い物かご価格ルール** 新しい価格ルールを作成します（詳細な手順については、を参照） [買い物かご価格ルールの作成](https://docs.magento.com/user-guide/marketing/price-rules-cart-create.html) （ユーザーガイドをご覧ください）。

   * クーポン コード = *特定のクーポン*.
   * 条件：小計が 25 ドル以上
   * アクション：送料無料= *品目が一致する出荷の場合*.

1. 23.10 ドルの価格で製品を作成します。
1. デフォルトの税務処理基準に CA 税を追加します。
1. この商品を買い物かごに追加します。
1. 送料の見積もりを取得します。税引き後、総計=$25.01 で、送料無料が適用されます。
1. クーポンコードを適用します – 小計（税別）が 23.10 ドルであるため、有効になりません。

<u>期待される結果</u>:

追加の構成設定として、「金額に税金を含める」があります。 *はい*/*不可* 送料無料の方法の設定では、次のようになります。

* 「金額に税金を含める」が「次」に設定されている場合 *はい*&#x200B;最小注文額は、小計+税 – 割引として計算されます。
* 「金額に税金を含める」が「次」に設定されている場合 *不可*&#x200B;の場合、最小注文額は小計 – 割引として計算されます。

<u>実際の結果</u>:

送料無料の価格ルール条件は小計に基づいてのみ設定でき、送料無料の方法は総計に基づいてのみ設定できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
