---
title: 「MDVA-37984：ステージングの更新が適用されている場合、ビジュアルマーチャンダイザーが正しく機能しない」
description: MDVA-37984 パッチを使用すると、ステージングアップデートが適用される際に、ビジュアルマーチャンダイザーの「製品をルールで一致させる」機能で製品が正しくフィルタリングされない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.9 がインストールされている場合に利用できます。 パッチ ID は MDVA-37984。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: d806b94c-3b22-4d4c-8afb-7b57a0ebfe46
feature: Categories, Merchandising, Products, Staging
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# MDVA-37984：ステージング更新が適用されている場合、ビジュアルマーチャンダイザーが正しく機能しない

MDVA-37984 パッチを使用すると、ステージングアップデートが適用される際に、ビジュアルマーチャンダイザーの「製品をルールで一致させる」機能で製品が正しくフィルタリングされない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.9 がインストールされている場合に使用できます。 パッチ ID は MDVA-37984。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ステージングアップデートが適用される場合、ビジュアルマーチャンダイザーの「ルールで製品を一致させる」機能で、製品が正しくフィルタリングされません。

<u> 再現手順 </u>:

1. 既存の製品のスケジュール更新を作成します。
   * `entity_id` と `row_id` に異なる値を設定します。
1. 新しい設定可能な製品を作成してから、単純な製品を作成します（新しい製品 `entity_id` と `row_ids` も異なります）。
   * 問題の再現を容易にするには、シンプルな製品に識別可能な数量の値（例：5000）を設定します。
1. カテゴリ/**カテゴリの製品** に移動し、「**ルールで製品を一致** を有効にします。
1. 次に、属性として「数量」、演算子として「より大きい」、値として「4500」を選択します。
1. **保存** をクリックします。

<u> 期待される結果 </u>:

新しく作成された設定可能なプロダクトがリストされます。

<u> 実際の結果 </u>:

新しく作成された設定可能なプロダクトはリストされません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
