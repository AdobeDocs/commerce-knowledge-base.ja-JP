---
title: 「MDVA-30972:REST API を使用して作成された注文ステータスの誤った出荷」
description: MDVA-30972 パッチは、REST API を使用した出荷作成時に注文ステータスが正しく変更されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。
exl-id: 70b8db1f-16d0-48f4-b0a2-483a7176cb89
feature: REST, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# MDVA-30972:REST API を使用して作成された注文ステータスの誤った出荷

MDVA-30972 パッチは、REST API を使用した出荷作成時に注文ステータスが正しく変更されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.7 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 から 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

*不正の疑い* 注文ステータスの注文について、管理者が REST API を使用して部分出荷を作成すると、注文ステータスが *処理中* に変更されます。 *不正行為の疑い* にとどまる必要があります。

<u> 前提条件 </u>:

* PayPal EC またはその他のオンライン支払い方法が設定されています。
* REST API の統合が設定されました。

<u> 再現手順 </u>:

1. 2 つ以上の項目で注文を作成します。
1. **管理者**/**営業**/**注文** にログインします。 作成した注文を開きます。
1. 注文詳細ページで、「注文合計 **までスクロールダウンし** す。 **ステータス** ドロップダウンをクリックし、*不正行為の疑い* を選択します。 次に、「**コメントを送信**」ボタンをクリックします。
1. 注文のステータスが *不正の疑い* であることを確認します。
1. REST API を使用して、注文から 1 つの品目の出荷を作成します。

   ```
   * Method = `Post`
   * Header = `"{host}/rest/V1/orders/ {order_id}/ship"`
   * Body =
   ```

   ```
    {      "items": [        {          "extension_attributes": {},          "order_item_id": {order_item_id},          "qty": 1        }      ]    }
   ```

1. Admin で注文を再度開き、ステータスを確認します。

<u> 期待される結果 </u>:

* 注文ステータス = *不正の疑い*。
* 同じ出荷が管理者から作成された場合、注文ステータスは変更されません。

<u> 実際の結果 </u>:

注文ステータス = *処理中*。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
