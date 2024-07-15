---
title: 「MDVA-35286：複数のアドレスをワンページチェックアウトに切り替え中にエラーが発生しました」
description: MDVA-35286 パッチでは、お客様がカートにバンドル製品を入れ、複数のアドレスのチェックアウトから Onepage のチェックアウトに切り替えるとエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.18 がインストールされている場合に利用できます。 パッチ ID は MDVA-35286。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 40c98735-6054-4b25-9882-e274424b203f
feature: Checkout, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# MDVA-35286：複数のアドレスからワンページ チェックアウトへの切り替えエラー

MDVA-35286 パッチでは、お客様がカートにバンドル製品を入れ、複数のアドレスのチェックアウトから Onepage のチェックアウトに切り替えるとエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.18 がインストールされている場合に使用できます。 パッチ ID は MDVA-35286。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.0-2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

買い物かごにバンドル製品があり、ユーザーが複数出荷のチェックアウトを放棄した後に、ワンページチェックアウトを使用しようとすると、エラーが表示されます。

<u> 再現手順 </u>:

1. 顧客アカウントにログインし、複数のバンドル製品を買い物かごに追加します。
1. リンクをクリックし、買い物かごを表示して編集します。
1. 「**複数のアドレスをチェックアウト**」リンクをクリックします。
1. 買い物かごに追加される製品に対して異なるアドレスを選択します。
1. **買い物かごに戻る** をクリックします。
1. カートで、「チェックアウトに進む **をクリックし** す。

<u> 期待される結果 </u>:

チェックアウトページにリダイレクトされます。

<u> 実際の結果 </u>:

「*リクエストの処理中にエラーが発生しました*」というエラーメッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
