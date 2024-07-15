---
title: 「MDVA-32449：販売注文履歴が遅いか、503 エラーで読み込まれない」
description: MDVA-32449 パッチを適用すると、Adobe Commerceで注文履歴の読み込みに時間がかかるか、読み込まれず、503 エラーが表示される問題が解決されます。 これは、13000+の顧客が B2B 会社に割り当てられている場合の問題です。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.12 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.1 で修正されました。
exl-id: e3fd4db2-b706-4712-ba8e-270eaca7fdb2
feature: B2B, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# MDVA-32449：販売注文履歴が遅いか、503 エラーで読み込まれない

MDVA-32449 パッチを適用すると、Adobe Commerceで注文履歴の読み込みに時間がかかるか、読み込まれず、503 エラーが表示される問題が解決されます。 これは、13000+の顧客が B2B 会社に割り当てられている場合の問題です。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.12 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.1 で修正されました。

## 影響を受ける製品とバージョン

これは、13000+の顧客が B2B 会社に割り当てられている場合の問題です。

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.3.5-p2、2.4.0、2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文履歴の読み込みに時間がかかる、またはまったく読み込まれない問題を修正しました。

<u> 前提条件 </u>:

B2B 会社に割り当てられた 13000 以上の顧客

<u> 再現手順 </u>:

1. 会社管理者としてストアフロントにログインします。
1. 販売注文履歴ページに移動します。

<u> 期待される結果 </u>:

「受注履歴」ページは通常どおりロードされます。

<u> 実際の結果 </u>:

ページの読み込みに時間がかかる。または、ページが読み込まれず、タイムアウトエラーが表示される。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
