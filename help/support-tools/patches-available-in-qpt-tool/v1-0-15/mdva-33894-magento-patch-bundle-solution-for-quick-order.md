---
title: 'MDVA-33894 パッチ：Quick Order 用のバンドルソリューション'
description: MDVA-33894 パッチでは、複数の製品の追加や削除、SKU の大文字と小文字の区別など、クイックオーダー機能に関する複数の問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.15 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: d0b18e71-5f48-441e-a8b9-c459f3d34599
feature: Cache, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# MDVA-33894 パッチ：クイック オーダー用バンドル ソリューション

MDVA-33894 パッチでは、複数の製品の追加や削除、SKU の大文字と小文字の区別など、クイックオーダー機能に関する複数の問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.15 がインストールされています。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.4.0-2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

MDVA-33894 パッチは、次の問題を修正したバンドルソリューションです。

* **マイアカウント** > **SKU で並べ替え** 機能では大文字と小文字が区別されます。有効な SKU を入力しても、大文字と小文字が正しくない場合（小文字ではなく大文字など）、Adobe Commerceはエラーをスローします。
* 買い物客が Quick Order を使用して買い物かごに複数の製品を追加し、製品を削除しようとすると、製品が削除されません。
* 複数の SKU を一括注文に追加する場合の大文字と小文字の区別に関する問題。
* 以前に入力された SKU でのクイックオーダーページキャッシュの問題。
* クイックオーダー数量は買い物かごに反映されません。
* SKU の重複が正しく検証されていません。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
