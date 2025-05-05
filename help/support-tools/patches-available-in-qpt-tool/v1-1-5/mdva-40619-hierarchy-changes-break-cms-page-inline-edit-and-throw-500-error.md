---
title: 「MDVA-40619：階層の変更により、CMS ページのインライン編集が中断され、500 エラーがスローされる」
description: MDVA-40619 パッチは、CMSのページ階層が変更されると、CMSのページのインライン編集が中断され、「500 エラー」がスローされる問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-40619。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: c003d845-1ba0-49c0-9f1a-a4b0ec00f30c
feature: CMS
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# MDVA-40619：階層の変更により、CMS ページのインライン編集が中断され、500 エラーがスローされる

MDVA-40619 パッチは、CMSのページ階層が変更されると、CMSのページのインライン編集が中断され、「500 エラー」がスローされる問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.5 がインストールされている場合に使用できます。 パッチ ID は MDVA-40619。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

CMS ページの階層が変更されると、CMS ページのインライン編集が機能しなくなり、「500 エラー」がスローされる。

<u> 再現手順 </u>:

1. 管理パネル/**コンテンツ**/**階層** に移動します。
1. 「デフォルトのストア表示」を選択します。
1. 「親ノード階層を使用」のチェックを外します。
1. ページを手動で選択し、「**保存** をクリックします。
1. 次に、**コンテンツ**/**ページ** に移動します。
1. グリッドから任意のCMSページを編集してみます。
1. **保存** をクリックします。

<u> 期待される結果 </u>:

ページが正常に保存されました。

<u> 実際の結果 </u>:

次のエラーが発生します。

*サーバーの技術的な問題によりエラーが発生しました。 やり直して、今までの作業を続けてください。 問題が解決しない場合は、後でもう一度試してください。*

`Error: Call to a member function getData() on null in /magento2ee/app/code/Magento/VersionsCms/Controller/Adminhtml/Cms/Page/InlineEdit/Plugin.php:62`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
