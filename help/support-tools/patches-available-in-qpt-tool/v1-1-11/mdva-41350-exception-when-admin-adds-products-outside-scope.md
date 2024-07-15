---
title: 「MDVA-41350：管理者がアクセス権の範囲外の製品を追加した場合の例外」
description: MDVA-41350 パッチでは、管理者ユーザーがアクセス権の範囲外にある製品を SKU で注文に追加すると、限定アクセス通知ではなく例外エラーがスローされる問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.11 がインストールされている場合に利用できます。 パッチ ID は MDVA-41350。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 3a96d029-5350-4dd6-aad3-2f2cdd5e65ac
feature: Admin Workspace, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# MDVA-41350：管理者がアクセス権の範囲外の製品を追加した場合の例外

MDVA-41350 パッチでは、管理者ユーザーがアクセス権の範囲外にある製品を SKU で注文に追加すると、限定アクセス通知ではなく例外エラーがスローされる問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.11 がインストールされている場合に使用できます。 パッチ ID は MDVA-41350。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

制限付きアクセスを使用する管理者ユーザーが、アクセス権の範囲外の SKU によって製品を順に追加すると、制限付きアクセスをユーザーに通知するメッセージの代わりに、例外が発生します。

<u> 再現手順 </u>:

1. 特定の web サイトにのみアクセスできるユーザーとして管理者にログインします。
1. **Sales**/**Orders** に移動し、「**Create New Order**」をクリックします。
1. 顧客およびストア表示を選択します。
1. **SKU による製品の追加** をクリックします。
1. どの web サイトにも割り当てられていない、または自分がアクセス権を持つ web サイトにも割り当てられていない SKU を検索します。
1. **注文に追加** をクリックします。

<u> 期待される結果 </u>:

適切なエラーメッセージが表示されます。

<u> 実際の結果 </u>:

例外が発生します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
