---
title: 「MDVA-33704 パッチ：店舗内ピックアップが表示されない」
description: MDVA-33704 パッチを適用すると、店舗内ピックアップ オプションを備えた製品が出荷方法として表示されない問題が解決されます。
exl-id: 2c5c7627-5d2e-44d2-9579-314dbd31ee8b
feature: Shipping/Delivery
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# MDVA-33704 パッチ：店舗内ピックアップが表示されない

MDVA-33704 パッチを適用すると、店舗内ピックアップ オプションを備えた製品が出荷方法として表示されない問題が解決されます。

このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.19 がインストールされています。 パッチ ID は MDVA-33704。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー上のAdobe Commerce 2.4.0-p1

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.0-2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>前提条件</u>:<br>

**店舗で選択** enabled

<u>再現手順</u>:

1. 商品を買い物かごに追加します。
1. チェックアウトに移動します。
1. 配送情報を追加し、店頭での受け取り以外の配送方法を選択します。
1. を選択 **支払いに進む**&#x200B;しかし、その後、支払いページに進まないでください。
1. 代わりに、に戻ります **連絡先と送料** セクション。
1. を選択 **ピックアップ**.
1. を選択 **ストア** および **クリックして支払い**.
1. 配送先住所は自動的に請求先住所として入力されます。
1. Web ページを更新します。

<u>期待される結果</u>:

店舗での受け取りオプションは、期待どおりに発送方法として表示されます。

<u>実際の結果</u>:

店舗での受け取りオプションは、配送方法として表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
