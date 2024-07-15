---
title: 「MDVA-44703：注文レポートの注文合計が正しく計算されない」
description: MDVA-44703 パッチは、制限された管理者ユーザーに対して、注文レポート内の注文合計が誤って計算される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.16 がインストールされている場合に利用できます。 パッチ ID は MDVA-44703。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: d8c31e47-ace6-4dba-a57c-941e722a6aad
feature: Orders
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# MDVA-44703：注文レポートの注文合計が正しく計算されない

MDVA-44703 パッチは、制限された管理者ユーザーに対して、注文レポート内の注文合計が誤って計算される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.16 がインストールされている場合に使用できます。 パッチ ID は MDVA-44703。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文レポートの注文合計が、制限された管理者ユーザーに対して誤って計算されます。

<u> 再現手順 </u>:

1. 2 つのストアを持つ追加の web サイトを作成します。
1. 新しい web サイトへのアクセス権のみを持つ、制限付きの管理者ユーザーを作成します。
1. 制限付きの管理者ユーザーとしてログインします。
1. 合計が異なる 2 つの注文を作成し、新規店舗ごとに 1 つずつ作成します。
1. 注文の請求書を作成します。
1. **レポート**/**売上** に移動し、**注文レポート** を開きます。
1. 統計を更新します。
1. 各ストアのレポートを参照してください。

<u> 期待される結果 </u>:

売上合計は、各店舗の注文金額に対応しています。

<u> 実際の結果 </u>:

サイト全体の集計売上高は、店舗ごとに表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
