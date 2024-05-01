---
title: 「MDVA-43983:「個別に表示されない」と設定されている製品が検索結果に表示される」
description: MDVA-43983 パッチを適用すると、「個別に表示されない」に設定されている製品がカタログの詳細検索結果に表示されたままになる問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.14 がインストールされている場合に利用できます。 パッチ ID は MDVA-43983。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 2599fb6c-5b27-461b-9740-f586ae7df9f5
feature: Catalog Management, Products, Search
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# MDVA-43983:[ 個別に表示されない ] に設定された製品が検索結果に表示される

MDVA-43983 パッチを適用すると、「個別に表示されない」に設定されている製品がカタログの詳細検索結果に表示されたままになる問題が解決されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.14 がインストールされています。 パッチ ID は MDVA-43983。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「個別に表示されない」に設定されている製品は、カタログの詳細検索結果に表示されます。

<u>再現手順</u>:

1. を使用した属性の作成 **店舗所有者のカタログ入力タイプ** as **ドロップダウン** または **ビジュアルスウォッチ** （例：カラー）。
1. を設定 **検索で使用** as **はい** および **詳細検索に表示** as **はい**.
1. 属性オプションをいくつか追加します。
1. を使用した製品の作成 **可視性** as **個別に表示されない**.
1. カラーアトリビュート オプションの割り当て。
1. に移動します **カタログの詳細検索** ストアフロントのページ。
1. カラー属性フィールドからカラー属性オプションのみを選択し、残りのフィールドは空白または空白のままにします。
1. 詳細検索フォームを送信します。
1. 検索結果を確認します。

<u>期待される結果</u>:

「個別に表示されない」と設定されている製品は、カタログの詳細検索結果に表示されません。

<u>実際の結果</u>:

「個別に表示されない」に設定されている製品は、カタログの詳細検索結果に表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
