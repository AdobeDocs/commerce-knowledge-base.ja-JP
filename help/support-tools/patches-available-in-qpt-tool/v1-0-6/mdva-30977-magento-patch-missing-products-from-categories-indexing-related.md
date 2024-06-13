---
title: 「MDVA-30977：カテゴリに製品が見つからない、インデックス関連」
description: MDVA-30977 パッチは、多数の製品で再インデックスまたは一括アクション中にストアフロントのカテゴリ ページに表示される製品の問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） v.1.0.6 がインストールされている場合に利用できます。 この問題は、Adobe Commerce 2.4.2 で修正される予定です。
exl-id: 66ec4f53-c01d-4f87-a175-84f44a26f5d3
feature: Categories, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# MDVA-30977: カテゴリに製品が見つからない、インデックス関連

MDVA-30977 パッチは、多数の製品で再インデックスまたは一括アクション中にストアフロントのカテゴリ ページに表示される製品の問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) v.1.0.6 がインストールされている。 この問題は、Adobe Commerce 2.4.2 で修正される予定です。

## 影響を受ける製品とバージョン

このパッチは、Cloud Infrastructure 2.3.4 上のAdobe Commerce用に作成されました。また、Adobe Commerce オンプレミス 2.3.4 とも互換性があります。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

### 問題 1

ストアフロントのカテゴリページに表示される製品数は、製品の一括更新時にページをリロードするたびに異なります。

<u>再現手順：</u>

1. 2 つのカテゴリに少なくとも 30000 個の製品を作成します。各カテゴリに少なくとも 15000 個の製品を作成します。
1. に移動 **カタログ** > **製品** Commerce Admin.
1. グリッドからすべての製品を選択し、属性の一括更新を実行します。 例えば、 **新規** = *はい* 属性。
1. を使用したMagento cron ジョブの実行 `bin/magento cron:run` コマンドを 2 回実行します。
1. Adobe Commerceが商品の更新を実行している間に、ストアフロントのカテゴリページ 30000 更新します。

<u>期待される結果：</u>

カテゴリ内の製品数は、カテゴリページを更新するたびに 15000 まります。

<u>実際の結果：</u>

カテゴリ内の製品数は、カテゴリページの更新ごとに異なります。

### 問題 2

インベントリの完全な再インデックスが実行されると、カテゴリページが空になり、 *選択内容に一致する製品が見つかりません* メッセージが表示されます。

<u>再現手順：</u>

1. Adobe CommerceにElasticsearchを設定します。
1. 新しい web サイトを追加します。
1. 新しいソースを作成し、「在庫を管理」を使用して新しい web サイトに割り当てます。
1. 設定可能な製品 30000 作成します。
1. すべての製品を新しい web サイトに割り当て、在庫を新しい在庫ソースに追加します。
1. 完全な再インデックスを実行します。
1. 次を実行して、インベントリの再インデックスを実行します。 `bin/magento indexer:reindex inventory`
1. 多数の商品があるカテゴリを参照します。

<u>期待される結果：</u>

カテゴリページでは、再インデックス時に通常どおり製品が表示されます。

<u>実際の結果：</u>

再インデックス中にカテゴリページが空になります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
