---
title: 「MDVA-42046：製品属性に割り当てられた値が正しくありません」
description: MDVA-42046 パッチでは、日付入力フィールドを持つ製品の更新時に、製品属性に誤った値が割り当てられる問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.13 がインストールされている場合に利用できます。 パッチ ID は MDVA-42046。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 837f5582-849c-43a3-ae02-87f71fb96061
feature: Attributes, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# MDVA-42046：製品属性に割り当てられた値が正しくありません

MDVA-42046 パッチでは、日付入力フィールドを持つ製品の更新時に、製品属性に誤った値が割り当てられる問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.13 がインストールされている場合に使用できます。 パッチ ID は MDVA-42046。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 ～ 2.3.5-p2 および 2.4.0 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`news_from_date` または `news_to_date` のフィールドを使用して製品を保存すると、これらのフィールドの値がデフォルトにリセットされます。

<u> 再現手順 </u>:

1. シンプルな製品を作成します。
1. 手順 1 で作成した製品をエクスポートします。
1. 書き出された CSV ファイルで、「`news_from_date`」および「`news_to_date`」フィールドに値を入力します。 例えば、2021-05-15 や 2021-06-18 などです。
1. 変更した CSV ファイルを使用して製品を読み込みます。
1. 製品グリッドに、「製品を新規開始日に設定」および「製品を新規終了日に設定」の列を追加します。
1. 製品の編集ページを開き、変更せずに **保存** をクリックします。
1. 製品グリッドに戻り、製品のデータを確認します。

<u> 期待される結果 </u>:

「製品を新規開始日に設定」と「製品を新規終了日に設定」は、保存前と同じです。

<u> 実際の結果 </u>:

* 「製品を新しい開始日に設定」列と「製品を新しい終了日に設定」列の値が変更されました。

* 「製品を新規開始日として設定」列には現在の日付が表示され、「製品を新規終了日として設定」列には何も表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
