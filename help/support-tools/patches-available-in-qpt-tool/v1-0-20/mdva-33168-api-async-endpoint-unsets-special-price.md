---
title: 「MDVA-33168:API 非同期エンドポイントが特別価格を解除する」
description: MDVA-33168 パッチは、API 非同期エンドポイントを使用して製品属性を更新すると、特別な価格が設定されなくなる問題を修正します。
exl-id: 4dd26215-b140-4924-8f4d-0d062e5fda2d
feature: REST, Orders, Personalization
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# MDVA-33168: API 非同期エンドポイントで特別価格の設定が解除されました

MDVA-33168 パッチは、API 非同期エンドポイントを使用して製品属性を更新すると、特別な価格が設定されなくなる問題を修正します。

このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.20 がインストールされている場合に使用できます。 パッチ ID は MDVA-33168。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.3-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.3 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. ストアを含む 2 つの web サイトを作成します。
1. **Stores/Configurations/Catalog/Catalog/Price/Catalog** に移動し、**Price Scope**=*Website* と設定します。
1. *text-type* 製品属性を作成します。 すべてのオプションはデフォルトのままにします。
1. 作成した属性をデフォルトの属性セットに追加します。
1. バンドル製品と共に使用するシンプルな製品を作成します。
1. 次のサンプルオプションを使用してバンドル製品を作成します。
   * **製品を有効にする** = *はい*。
   * **属性セット** = *デフォルト*。
   * **製品名** = *bundle-1*。
   * **SKU** = *bundle-1*。
   * **動的 SKU** = *はい*。
   * **価格**=100 *ドル*。
   * **税区分** = *課税品*。
   * **在庫状況** = *在庫*。
1. **バンドル項目** の下で、次のサンプルオプションを設定します。
   * **バンドル品目を出荷** = *一緒*。
   * **オプションタイトル** = *テスト*、**入力タイプ** = *ラジオボタン*、**必須** チェックボックス = *オン*。
   * **デフォルトです** checkbox = *オフ*。
   * **名前** = *simple-100*。
   * **SKU** = *simple-100*。
   * **価格**=100.00 *ド*。
   * **価格タイプ** = *固定*。
   * **既定の数量** = *1*。
   * **ユーザー定義** チェックボックス = *オフ*。
1. 範囲をデフォルト以外の店舗に切り替え、特別価格を設定します。 （例：**詳細価格** ページで、**特別価格** = *4%*、**価格表示** = *価格範囲* と設定します。）
1. 次の例のように、デフォルト以外のストアスコープでのみ新しい属性を更新します。

   ```php
       PUT {{base_url}}/rest/en_au/async/V1/products/{{sku}}    {        "product": {            "custom_attributes": [                {                    "attribute_code": "text_attr",                    "value": 21                                   }            ]                    }    }
   ```

<u> 期待される結果 </u>:

非同期 rest API を使用して製品属性を更新する場合、他の属性値は期待どおりに同じままです。

<u> 実際の結果 </u>:

ストアスコープで非同期 rest API を使用して設定された特別価格が削除されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
