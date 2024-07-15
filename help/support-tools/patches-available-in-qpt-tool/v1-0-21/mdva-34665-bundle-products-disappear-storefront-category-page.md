---
title: 「MDVA-34665：バンドル製品がストアフロントのカテゴリページを表示しなくなる」
description: MDVA-34665 パッチは、カテゴリ ページにバンドルされた製品が見つからない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.21 がインストールされている場合に利用できます。 パッチ ID は MDVA-34665。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: 2b393f91-de0d-4c54-89db-5e2af13f93a6
feature: Categories, Products, Storefront
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# MDVA-34665：バンドル製品がストアフロントのカテゴリページに表示されない

MDVA-34665 パッチは、カテゴリ ページにバンドルされた製品が見つからない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.21 がインストールされている場合に使用できます。 パッチ ID は MDVA-34665。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.4-2.3.4-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

**ケース 1:**

<u> 前提条件 </u>:

1. 1 つのシンプルな製品をバンドルオプションとして使用し、15,000 個のバンドル製品を作成します。 複数のバンドル製品で同じシンプルな製品を使用しないでください。
1. シンプルな製品は、「*個別に表示されない* に設定する必要があります。

<u> 再現手順 </u>:

1. 15,000 個のバンドル製品を、それぞれ 7,500 個の 2 つのカテゴリに割り当てます。
1. すべてのシンプルな製品（15k）を選択し、製品質量属性のアップデートを使用して在庫を更新します。 検索 cl テーブルに多数の ID を含めることを目標としています（cl テーブルは、インデクサーがどのレコードを更新する必要があるかを知るために使用するテーブルです）。
1. `catalogsearch_fulltext_cl` テーブルに 15,000 個の ID があることを確認します。
1. `indexer_update_all_views` インデクサーが実行されていることを確認します。
1. カテゴリページに対して継続的にクエリを実行し、製品数を確認します。

<u> 期待される結果 </u>:

製品数は、インデックス再作成後と同じままになります。

<u> 実際の結果 </u>:

製品カウントは、しばらくすると 7,450 に低下します。 インデックス作成が完了した後も、7,450 個のままです。

**ケース 2:**

<u> 再現手順 </u>:

1. 関連付けられたシンプルな製品をオプションとして持つバンドル製品を作成します。
1. インデクサーモードを *スケジュールに従って更新* に変更します。
1. バンドル製品をカテゴリに割り当てます。
1. シンプル製品の在庫状態を *在庫切れ* に変更します。
1. Cron を実行します。バンドル製品がストアフロントに表示されなくなります。
1. シンプルな商品に在庫を追加して保存します。
1. Cron インデクサーを実行します。
1. カテゴリ ページを更新します。

<u> 期待される結果 </u>:

製品はまだ存在しません。

<u> 実際の結果 </u>:

バンドル製品が再び表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
