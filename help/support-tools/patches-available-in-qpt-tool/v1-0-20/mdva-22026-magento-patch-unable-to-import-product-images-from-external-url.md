---
title: 「MDVA-22026：製品イメージを外部 URL からインポートできない」
description: MDVA-22026 パッチでは、外部 URL から製品画像をインポートできない問題が修正されています。
exl-id: 29043c6c-daf2-4925-85bf-49eeeee3742c
feature: Data Import/Export, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# MDVA-22026：外部 URL から製品画像をインポートできない

MDVA-22026 パッチでは、外部 URL から製品画像をインポートできない問題が修正されています。

このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.20 がインストールされている場合に使用できます。 パッチ ID は MDVA-22026。 この問題は、Adobe Commerce バージョン 2.3.4 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.2-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.2-2.3.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. 管理者で、**システム**/**読み込み** に移動します。
1. **エンティティタイプ** = *製品* を設定します。
1. **読み込み動作** = *追加/更新* を設定します。
1. **許可されたエラー数** = *10000* を設定します。
1. 読み込むファイルを選択します。
1. 「**データを確認**」ボタンをクリックします（ファイルを検証する必要があります）。
1. 「**インポート**」ボタンをクリックします。

<u> 期待される結果 </u>:

外部 URL からの画像を含む、CSV ファイルからの製品の読み込みが期待どおりに完了しました。

<u> 実際の結果 </u>:

外部 URL からの画像を含む、CSV ファイルからの製品の読み込みに失敗し、同様のエラーが表示されます。

```php
1. Imported resource (image) could not be downloaded from external resource due to timeout or access permissions in row(s): 4, 5, 8, 9, 16, 18, 20, 21, 22, 23, 26, 27, 28, 52, 53, 55, 58, 63, 70, 71, 77, 78, 83, 84, 91
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはオンプレミスのMagento Open Source: [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html)
* クラウドインフラストラクチャー上のAdobe Commerce: [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool でAdobe Commerceの問題をチェックしてください ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
