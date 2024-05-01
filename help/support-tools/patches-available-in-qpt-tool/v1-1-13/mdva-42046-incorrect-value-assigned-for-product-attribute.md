---
title: 「MDVA-42046：製品属性に割り当てられた値が正しくありません」
description: MDVA-42046 パッチでは、日付入力フィールドを持つ製品の更新時に、製品属性に誤った値が割り当てられる問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.13 がインストールされている場合に利用できます。 パッチ ID は MDVA-42046。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 837f5582-849c-43a3-ae02-87f71fb96061
feature: Attributes, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# MDVA-42046：製品属性に割り当てられた値が正しくありません

MDVA-42046 パッチでは、日付入力フィールドを持つ製品の更新時に、製品属性に誤った値が割り当てられる問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.13 がインストールされています。 パッチ ID は MDVA-42046。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 ～ 2.3.5-p2 および 2.4.0 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

での製品の保存後 `news_from_date` および/または `news_to_date` フィールドの場合、これらのフィールドの値がデフォルトにリセットされます。

<u>再現手順</u>:

1. シンプルな製品を作成します。
1. 手順 1 で作成した製品をエクスポートします。
1. 書き出された CSV ファイルで、 `news_from_date` および `news_to_date` フィールド。 例えば、2021-05-15 や 2021-06-18 などです。
1. 変更した CSV ファイルを使用して製品を読み込みます。
1. 製品グリッドに、「製品を新規開始日に設定」および「製品を新規終了日に設定」の列を追加します。
1. 製品の編集ページを開き、変更せずに、 **保存**.
1. 製品グリッドに戻り、製品のデータを確認します。

<u>期待される結果</u>:

「製品を新規開始日に設定」と「製品を新規終了日に設定」は、保存前と同じです。

<u>実際の結果</u>:

* 「製品を新しい開始日に設定」列と「製品を新しい終了日に設定」列の値が変更されました。

* 「製品を新規開始日として設定」列には現在の日付が表示され、「製品を新規終了日として設定」列には何も表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
