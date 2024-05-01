---
title: 「MDVA-44044：新しい web サイトに割り当てられた後、製品がカテゴリページに表示されない」
description: MDVA-44044 パッチを適用すると、新しい Web サイトに製品を割り当てた後、製品がカテゴリ ページに表示されない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.16 がインストールされている場合に利用できます。 パッチ ID は MDVA-44044。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: e3a179ed-243c-4200-a01a-796657bd31ab
feature: Categories, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# MDVA-44044：製品が新しい Web サイトに割り当てられた後、カテゴリページに表示されない

MDVA-44044 パッチを適用すると、新しい Web サイトに製品を割り当てた後、製品がカテゴリ ページに表示されない問題が解決されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.16 がインストールされています。 パッチ ID は MDVA-44044。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品を新しい web サイトに割り当てると、カテゴリページに製品が表示されません。

<u>再現手順</u>:

1. インデクサーモードをスケジュールに設定します。
1. セカンダリ web サイト、ストア、ストア表示を作成します。
1. にセカンダリストアコードを追加します `index.php`:

   ```php
   $_SERVER["MAGE_RUN_CODE"]="en_us";
   $_SERVER["MAGE_RUN_TYPE"]="store";
   ```

1. 新しいカテゴリを作成します。
1. 新しく作成されたカテゴリに割り当てる新しい製品を作成します。 必ずプライマリ web サイトにのみ割り当ててください。
1. cron を実行します。
1. ストアフロントからカテゴリを開きます。
1. 製品をセカンダリ web サイトに割り当てます。
1. cron を再度実行します。

<u>期待される結果</u>:

スケジュールされたインデクサーの後、製品がカテゴリページに表示されます。

<u>実際の結果</u>:

製品は、完全に再インデックス化されるまで、カテゴリページに表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
