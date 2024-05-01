---
title: 「ACSD-51899：デフォルトの配送先住所が正しく自動入力されない」
description: ACSD-51899 パッチを適用すると、デフォルトの配送先住所に間違った住所が自動入力されるAdobe Commerceの問題を修正できます。
feature: Checkout
role: Admin
exl-id: 67100fcd-e98f-4740-8f1f-fcc820f4c75d
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# ACSD-51899：デフォルトの配送先住所が正しく自動入力されない

ACSD-51899 パッチは、デフォルトの配送先住所が間違った住所で自動入力される問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-51899 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

デフォルトの配送先住所は、間違った住所で自動入力されます

<u>再現手順</u>:

1. Enable （有効） **店舗での受け取り** 配送方法に従います。
1. 作成 *在庫* および *ソース*.
1. 製品を作成し、製品をソースに割り当てます。
1. 商品を買い物かごに追加します。
1. クリックする **チェックアウトに進む** ミニカートから。
1. テストメールアドレスを入力して選択 **店舗で選択**.
1. 「」をクリックします **ストアを選択** ボタンをクリックし、選択するストアの場所を選択します。
1. 「」をクリック **次へ** ボタン。
1. に移動します。 **ホームページ** ストアのロゴをクリックすることで。
1. を開きます **ミニカート**.
1. という名前の下部のハイパーリンクをクリックします。 **買い物かごの表示と編集**.
1. クリック **チェックアウトに進む**.
1. [ 配送 ] ページの [ 配送 ] ボタンをクリックします。

<u>期待される結果</u>

配送先住所フィールドは、を除き空のままです *国、地域、郵便番号*.

<u>実際の結果</u>

デフォルトの配送先住所には、が自動入力されます *店舗での受け取り* ページを更新した後のアドレス。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
