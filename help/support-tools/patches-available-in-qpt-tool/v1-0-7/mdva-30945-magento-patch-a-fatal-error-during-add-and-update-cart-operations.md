---
title: 「MDVA-30945：買い物かごへの追加および更新操作中の致命的なエラー」
description: MDVA-30945 パッチは、カートの更新時に module-configurable-product CartItemProcessor.php*でメンバ関数 getValue （）の呼び出しが null の場合に致命的なエラー*が発生する問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 この問題は、Adobe Commerce 2.4.2 で修正されました。
exl-id: 0950e91b-900b-421d-91e7-abbfca4f30be
feature: Orders, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# MDVA-30945：買い物かごへの追加および更新操作中に致命的なエラーが発生する

MDVA-30945 パッチは、買い物かごの更新時に致命的なエラー *モジュール – configurable-product CartItemProcessor.php のメンバ関数 getValue （）の呼び出しが null の場合* を受け取る問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.7 がインストールされている場合に使用できます。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カート内の製品が管理者で更新された後に発生した、致命的な PHP エラー。

<u> 再現手順 </u>:

1. Commerce管理者で、オプションを指定せずに設定可能な商品を作成します。
1. それをストアフロントのカートに追加します。
1. 管理者に戻り、設定可能なオプションを製品に追加して、変更を保存します。
1. ストアフロントで買い物かごページを更新します。

<u> 期待される結果 </u>:

買い物かごページに、次の検証メッセージが表示されます。*以下の製品の一部には、必要なオプションがすべて用意されていません*。

<u> 実際の結果 </u>:

買い物かごページが空白になる。 PHP `error.log` では、次のエラーがログに記録されます。*Uncaught exception &#39;Error&#39; with message &#39;Call to a member function getValue （） on null&#39; in vendor/magento/module-configurable-product/Model/Quote/Item/CartItemProcessor.php:76*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
