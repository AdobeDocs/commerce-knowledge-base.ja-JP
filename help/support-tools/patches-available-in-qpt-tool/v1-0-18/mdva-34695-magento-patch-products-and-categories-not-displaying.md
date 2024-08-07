---
title: 「MDVA-34695：製品とカテゴリが表示されない」
description: MDVA-34695 パッチを使用すると、製品とカテゴリが管理のカテゴリグリッドに表示されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.18 がインストールされている場合に利用できます。 パッチ ID は MDVA-34695。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: 0c2e50c1-648b-480a-a768-72af721950d8
feature: Categories, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# MDVA-34695：製品とカテゴリが表示されない

MDVA-34695 パッチを使用すると、製品とカテゴリが管理のカテゴリグリッドに表示されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.18 がインストールされている場合に使用できます。 パッチ ID は MDVA-34695。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.4

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0-2.4.0-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カテゴリを削除すると、`children_count` の負の値がデータベースに表示されます。

<u> 再現手順 </u>:

1. 管理バックエンドにログインします。
1. **カタログ/カテゴリ** に移動します。
1. **サブカテゴリを追加** をクリックします。
1. **カテゴリ名** = *親 1* を設定し、「保存」を選択します。
1. **サブカテゴリを追加** をクリックします。
1. **カテゴリ名** = *子 1* を設定し、「保存」を選択します。
1. **サブカテゴリを追加** をクリックします。
1. **カテゴリ名** = *子 2* を設定し、保存します。
1. **サブカテゴリを追加** をクリックします。
1. **カテゴリ名** = *子 3* を設定し、保存します。 この時点で、このカテゴリのレベルは *5* である必要があります。
1. **子 1** カテゴリをクリックします。
1. カテゴリを削除します。

<u> 期待される結果 </u>:

カテゴリグリッドは、期待どおりに製品とカテゴリを表示します。

<u> 実際の結果 </u>:

カテゴリグリッドが空です。 データベース内の `catalog_category_entity` テーブルを確認します。 `children_count` が負になったことに注意してください。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
