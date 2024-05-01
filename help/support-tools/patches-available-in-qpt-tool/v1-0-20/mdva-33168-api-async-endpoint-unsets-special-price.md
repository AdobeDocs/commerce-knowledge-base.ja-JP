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

このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.20 がインストールされています。 パッチ ID は MDVA-33168。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.3-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.3 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. ストアを含む 2 つの web サイトを作成します。
1. に移動 **ストア/設定/カタログ/カタログ/価格/カタログ** と Set **価格範囲** = *Web サイト*.
1. を作成 *テキストタイプ* 製品属性。 すべてのオプションはデフォルトのままにします。
1. 作成した属性をデフォルトの属性セットに追加します。
1. バンドル製品と共に使用するシンプルな製品を作成します。
1. 次のサンプルオプションを使用してバンドル製品を作成します。
   * **製品を有効にする** = *はい*.
   * **属性セット** = *デフォルト*.
   * **製品名** = *bundle-1*.
   * **SKU** = *bundle-1*.
   * **動的 SKU** = *はい*.
   * **価格** = *100 ドル*.
   * **税クラス** = *課税品*.
   * **在庫ステータス** = *在庫あり*.
1. 次の下 **バンドル項目**&#x200B;で、次のオプション例を設定します。
   * **バンドル品目の出荷** = *連携*.
   * **オプションタイトル** = *テスト*, **入力タイプ** = *ラジオボタン*, **必須** チェックボックス = *確認済み*.
   * **デフォルト** チェックボックス = *未チェック*.
   * **名前** = *simple-100*.
   * **SKU** = *simple-100*.
   * **価格** = *100.00*.
   * **価格タイプ** = *固定*.
   * **既定の数量** = *1*.
   * **ユーザー定義** チェックボックス = *未チェック*.
1. 範囲をデフォルト以外の店舗に切り替え、特別価格を設定します。 （例： **詳細価格** ページ，設定 **特別価格** = *4%*、および **価格ビュー** = *価格範囲*.）
1. 次の例のように、デフォルト以外のストアスコープでのみ新しい属性を更新します。

   ```php
       PUT {{base_url}}/rest/en_au/async/V1/products/{{sku}}    {        "product": {            "custom_attributes": [                {                    "attribute_code": "text_attr",                    "value": 21                                   }            ]                    }    }
   ```

<u>期待される結果</u>:

非同期 rest API を使用して製品属性を更新する場合、他の属性値は期待どおりに同じままです。

<u>実際の結果</u>:

ストアスコープで非同期 rest API を使用して設定された特別価格が削除されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
