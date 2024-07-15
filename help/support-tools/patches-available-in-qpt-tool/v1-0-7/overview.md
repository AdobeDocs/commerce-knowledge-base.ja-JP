---
title: '概要： [!DNL Quality Patches Tool]  （QPT） v1.0.7'
description: このサブセクションでは、 [!DNL Quality Patches Tool]  （QPT） v1.0.7 で使用可能なパッチによって修正された問題について詳しく説明します。
exl-id: 2415ca7a-4aec-4a63-9ae9-ee7b29bbc8d7
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# [!DNL Quality Patches Tool] （QPT） v1.0.7 の概要

このサブセクションでは、[!DNL Quality Patches Tool] （QPT） v1.0.7 で使用可能なパッチによって修正された問題について詳しく説明します。

QPT v1.0.7 には、次のパッチが含まれています。

1. **MDVA-29148**:API 呼び出しを介して製品を作成する際に、ペイロードに値が指定されていない場合、`\Magento\Eav\Model\Entity\Attribute\Backend\ArrayBackend` （Multiselect など）タイプの製品カスタム属性がデフォルト値を使用しない問題を修正。
1. **MDVA-29389**：詳細レポートで、`analytics_collect_data` cronjob が *Port はホストパラメーター内で設定する必要がある（localhost:3306 など）* と表示する問題を修正しました。
1. **MDVA-30594**:FPT が設定されている場合に、チェックアウト時に複数のアドレスを持つ注文を保存できなかった問題を修正しました。
1. **MDVA-30782**：買い物かごのルールに関係なく、動的ブロックが表示される問題を修正。
1. **MDVA-30815**：検索結果ページに表示する検索結果の数を変更した場合の問題を修正しました。
1. **MDVA-30837**：送料無料の計算に設定オプションを追加し、ユーザーが小計（または総計）に基づいて送料無料を受け取るための最小注文額を設定できるようにします。
1. **MDVA-30945**：買い物かごを `Call to a member function getValue() on null in module-configurable-product CartItemProcessor.php` に更新すると致命的なエラーメッセージが表示される問題を修正。
1. **MDVA-30972**:WebApi を使用した部分出荷作成後に、カスタム注文のステータスが *処理中* に変更される問題を修正しました。
1. **MDVA-31007**：カスタムアドレス属性がマイアカウント領域の注文詳細ページとバックエンドに正しく表示されない問題を修正しました。
1. **MDVA-31021**:`module-catalog-import-export/Model/Import/Product/Option.php` でパフォーマンスの問題が発生している問題を修正しました。 テーブルに 100,000 件を超えるレコードがある場合、1 つの製品 `catalog_product_option` 含む新しい CSV の検証に要する時間は 10 秒未満です。
1. **MDVA-31224**：バンドル製品の `catalog_product_price` の再インデックス操作のパフォーマンスを向上させます。
1. **MDVA-31282**:Adobe Commerceで [!DNL Paypal PayFlow Pro] に二重認証が発生する問題を修正。 二重認証は、不正フィルターをバイパスし、取引手数料 [!DNL PayFlow Pro's] 倍増する効果もあります。
1. **MDVA-31343**：カテゴリがスケジュールされているときに、削除された本文クラス `page-layout-category-full-width` の問題を修正します。

左側のメニューを使用して、特定のパッチページに移動します。
