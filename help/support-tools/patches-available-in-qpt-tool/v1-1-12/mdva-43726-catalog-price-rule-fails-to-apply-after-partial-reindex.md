---
title: 「MDVA-43726：部分的な再インデックス後にカタログ価格ルールの適用に失敗する」
description: MDVA-43726 パッチは、部分的な再インデックス後に、ストアレベル属性の一致に基づくカタログ価格ルールが適用されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-43726。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 70e7e1d2-e601-4fed-9274-a1a619de29e1
feature: Catalog Management, Categories, Orders, Price Rules
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# MDVA-43726：部分的な再インデックス後にカタログ価格ルールが適用されない

MDVA-43726 パッチは、部分的な再インデックス後に、ストアレベル属性の一致に基づくカタログ価格ルールが適用されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.12 がインストールされている場合に使用できます。 パッチ ID は MDVA-43726。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

部分的な再インデックス後に、ストアレベル属性の一致に基づくカタログ価格ルールが適用されない。

<u> 再現手順 </u>:

1. インデクサーモードをスケジュールどおりに実行するように設定します。
1. 設定可能な 2 つの製品属性を作成します。 例：カラー（ビジュアルスウォッチ）およびサイズ（テキストスウォッチ）。
1. 手順 2 で作成した両方の属性を使用して、設定可能な製品を作成します。
1. 製品を作成したら、**はい/いいえ** タイプの属性を作成して、ルール条件で表示できるようにします。
1. この属性をデフォルトの属性セットに追加します。
1. この属性が **はい** に設定されている場合に適用するカタログ価格ルールを作成します。
1. 設定可能な商品に関連するシンプルな商品の 1 つを開きます。
1. 範囲をストア表示に変更し、属性値を **はい** に更新します。
1. `CRON` を実行し、フロントエンドで価格を確認します。
1. 完全な再インデックスを実行します。 もう一度、フロントエンドの価格を確認してください。
1. 設定可能な製品カテゴリを更新します。
1. `CRON` を実行し、フロントエンドでもう一度価格を確認します。

<u> 期待される結果 </u>:

増分インデクサーを使用した完全な再インデックスを実行しない場合、カタログルールは正しく適用されます。

<u> 実際の結果 </u>:

完全な再インデックスを実行しないと、カタログルールは適用されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
