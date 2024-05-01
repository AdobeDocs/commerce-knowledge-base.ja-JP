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

MDVA-30945 パッチを適用すると、致命的なエラーが発生する問題が修正されます *module-configurable-product CartItemProcessor.php でメンバ関数 getValue （）を null で呼び出す* 買い物かごを更新する場合。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カート内の製品が管理者で更新された後に発生した、致命的な PHP エラー。

<u>再現手順</u>:

1. Commerce管理者で、オプションを指定せずに設定可能な商品を作成します。
1. それをストアフロントのカートに追加します。
1. 管理者に戻り、設定可能なオプションを製品に追加して、変更を保存します。
1. ストアフロントで買い物かごページを更新します。

<u>期待される結果</u>:

買い物かごページに、次の検証メッセージが表示されます。 *以下の製品の一部には、必要なオプションが用意されていません*.

<u>実際の結果</u>:

買い物かごページが空白になる。 PHP の場合 `error.log`を入力すると、次のエラーが記録されます。 *vendor/magento/module-configurable-product/Model/Quote/Item/CartItemProcessor.php:76 のメッセージ「null のメンバー関数 getValue （）への呼び出し」でキャッチできない例外「Error」*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
