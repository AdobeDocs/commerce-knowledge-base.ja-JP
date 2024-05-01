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

このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.20 がインストールされています。 パッチ ID は MDVA-22026。 この問題は、Adobe Commerce バージョン 2.3.4 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.3.2-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.2-2.3.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. 管理者で、に移動します。 **システム** > **インポート**.
1. を設定 **エンティティタイプ** = *製品*.
1. を設定 **読み込み動作** = *追加/更新*.
1. を設定 **許可されたエラー数** = *10000*.
1. 読み込むファイルを選択します。
1. 「」をクリックします **データを確認** ボタン（ファイルを検証する必要があります）。
1. 「」をクリックします **インポート** ボタン。

<u>期待される結果</u>:

外部 URL からの画像を含む、CSV ファイルからの製品の読み込みが期待どおりに完了しました。

<u>実際の結果</u>:

外部 URL からの画像を含む、CSV ファイルからの製品の読み込みに失敗し、同様のエラーが表示されます。

```php
1. Imported resource (image) could not be downloaded from external resource due to timeout or access permissions in row(s): 4, 5, 8, 9, 16, 18, 20, 21, 22, 23, 26, 27, 28, 52, 53, 55, 58, 63, 70, 71, 77, 78, 83, 84, 91
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html).
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html).

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md).
* [Quality Patches Tool を使用して、Adobe Commerceの問題のパッチを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md).

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
