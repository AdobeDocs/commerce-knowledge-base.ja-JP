---
title: 「ACSD-45849：ステージングアップデート後にビデオメタデータが失われる」
description: ACSD-45849 パッチは、ステージングアップデートの適用後にビデオのメタデータが失われる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.18 がインストールされている場合に利用できます。 パッチ ID は ACSD-45849 です。 この問題はAdobe Commerce 2.4.4 で修正されました。
exl-id: 071a535d-f96c-4731-a17c-0b7bf8a87372
feature: Staging, Page Content
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# ACSD-45849：ステージングアップデート後にビデオメタデータが失われる

ACSD-45849 パッチは、ステージングアップデートの適用後にビデオのメタデータが失われる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.18 がインストールされている場合に使用できます。 パッチ ID は ACSD-45849 です。 この問題はAdobe Commerce 2.4.4 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ステージングアップデートの適用後に、ビデオのメタデータが失われます。

<u> 再現手順 </u>:

1. **管理者**/**ストア**/**設定**/**カタログ**/**商品ビデオ** でYouTube API キーを設定します。
1. YouTube ビデオを使用して製品を作成します。 URL、タイトル、説明が入力されます。
1. 「*画像とビデオ*」セクションを変更せずに、パラメーターを含んだ新しいスケジュールされた商品アップデートを作成します。
1. スケジュールされた変更で **表示/編集** をクリックします。
1. **画像とビデオ** に移動し、ビデオをクリックします。

<u> 期待される結果 </u>:

URL、タイトル、説明には、適切なデータが含まれています。

<u> 実際の結果 </u>:

URL、タイトル、説明の各フィールドが空です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
