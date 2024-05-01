---
title: 「MDVA-23764 Magentoパッチ：ダイナミックブロックを読み込み中にエラーが発生しました」
description: MDVA-23764 Magento パッチは、のバグを修正します。
exl-id: b884ade6-f88d-4c79-8e84-5a59252abb75
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---

# MDVA-23764 Magento修正プログラム：ダイナミック ブロックの読み込み中にエラーが発生しました

MDVA-23764 Magento パッチは、のバグを修正します。

```php
JsFooterPlugin.php
```

これは、ダイナミック ブロックの表示に影響します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.13 がインストールされています。 この問題はMagento 2.3.5 で修正されました。

## 影響を受ける製品とバージョン

**Magentoバージョン用のパッチが作成されます。** Magento Commerce Cloud 2.3.3。

**Magentoバージョンとの互換性：** Magento CommerceとMagento Commerce Cloud 2.3.2 ～ 2.3.4-p2。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順：</u>

https://\[magento domain\]/banner/ajax/load/のような URL を読み込んでみます。

<u>実際の結果：</u>

次のようなエラーがスローされます。 *見つからなかった TypeError: strpos （）は、パラメーター 1 が文字列であることを想定しています。コードの行に null が指定されています* .

<u>期待される結果：</u>

URL はエラーなしで読み込まれます。

## パッチの適用

QPT パッチを適用する手順については、Magentoに応じて次のリンクを使用してください。

* Magento Commerce:DevDocs [品質向上パッチツールを使用したパッチの適用](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) .
* Magento Commerce Cloud:DevDocs [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) .

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) .
* [Quality Patches Tool を使用して、Magentoの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) .

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
