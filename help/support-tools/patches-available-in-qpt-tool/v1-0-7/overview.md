---
title: '概要： [!DNL Quality Patches Tool] （QPT） v1.0.7'
description: このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.0.7.
exl-id: 2415ca7a-4aec-4a63-9ae9-ee7b29bbc8d7
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# [!DNL Quality Patches Tool] （QPT） v1.0.7 の概要

このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.0.7.

QPT v1.0.7 には、次のパッチが含まれています。

1. **MDVA-29148**：の製品カスタム属性である API 呼び出しを使用して製品を作成する際の問題を修正しました `\Magento\Eav\Model\Entity\Attribute\Backend\ArrayBackend` （Multiselect と同様に）ペイロードに値が指定されていない場合、タイプはそのデフォルト値を使用しません。
1. **MDVA-29389**：詳細レポートで問題が修正された場合 `analytics_collect_data` cronjob の発言： *ポートは、ホストパラメーター（localhost:3306 など）内で設定する必要があります*.
1. **MDVA-30594**:FPT が設定されている場合、チェックアウト時に複数のアドレスを持つ注文を保存できなかった問題を修正しました。
1. **MDVA-30782**：買い物かごのルールに関係なく、動的ブロックが表示される問題を修正しました。
1. **MDVA-30815**：検索結果ページに表示する検索結果の数を変更した際の問題を修正しました。
1. **MDVA-30837**：送料無料の計算に設定オプションを追加します。これにより、ユーザーは小計（または総計）に基づいて送料無料を受け取るための最小注文額を設定できます。
1. **MDVA-30945**：買い物かごを更新すると致命的なエラーメッセージが表示される問題を修正しました `Call to a member function getValue() on null in module-configurable-product CartItemProcessor.php`.
1. **MDVA-30972**：カスタム注文のステータスがに変更される問題を修正しました *処理* webapi を使用した部分出荷作成後。
1. **MDVA-31007**：カスタムアドレス属性がマイアカウント領域の注文の詳細ページとバックエンドに正しく表示されない問題を修正しました。
1. **MDVA-31021**：でパフォーマンスの問題が発生している問題を修正しました `module-catalog-import-export/Model/Import/Product/Option.php`. に 100,000 件以上のレコードがある場合 `catalog_product_option` 表：単一製品の新しい CSV の検証に要する時間は 10 秒未満です。
1. **MDVA-31224**：のパフォーマンスを向上させます `catalog_product_price` バンドル製品の再インデックス操作。
1. **MDVA-31282**：二重承認が発生する問題を修正しました [!DNL Paypal PayFlow Pro] Adobe Commerceで。 二重認証には、バイパスする効果もあります [!DNL PayFlow Pro's] 不正フィルターと取引手数料の倍増。
1. **MDVA-31343**：削除された本文クラスの問題を修正しました `page-layout-category-full-width` カテゴリがスケジュールされたとき。

左側のメニューを使用して、特定のパッチページに移動します。
