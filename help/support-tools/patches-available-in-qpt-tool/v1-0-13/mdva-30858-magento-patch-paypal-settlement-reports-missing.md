---
title: 「MDVA-30858:PayPal 決済レポートが見つからない」
description: 「複数の PayPal アカウントを持っている場合、MDVA-30858 パッチは PayPal 決済レポートが欠落している問題を修正します。 レポートは、管理者サイドバーの&gt; **Reports** &gt; Sales &gt; **PayPal Settlement**から利用できます。 代わりに、「レコードが見つかりませんでした。」というメッセージが表示されます。*が表示されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.13 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。」
exl-id: 268aa74c-5cb5-4653-a6c9-1d4c30167e6a
feature: Orders, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# MDVA-30858: PayPal 決済レポートが見つからない

複数の PayPal アカウントを持っている場合、MDVA-30858 パッチは、PayPal 決済レポートが見つからない問題を修正します。 レポートは、管理者サイドバー/**レポート**/販売/**PayPal 決済** で使用できます。 代わりに、「*レコードが見つかりませんでした。* が表示されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.13 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.4

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数の PayPal アカウントを持っている場合に、**Reports**/Sales/**PayPal Settlement** でレコードが見つからなかった問題を修正しました。

<u> 再現手順 </u>:

1. PayPal 決済レポートを設定します。
1. 管理者に移動し、**レポート**/売上/**PayPal 決済** に移動します。
1. 最新の更新を取得するには、右上隅にある **更新を取得** をクリックします。

<u> 期待される結果 </u>:

レポートが表示されます。

<u> 実際の結果 </u>:

レポートは使用可能ですが、グリッドには何も表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
