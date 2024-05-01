---
title: 「MDVA-43726：部分的な再インデックス後にカタログ価格ルールの適用に失敗する」
description: MDVA-43726 パッチは、部分的な再インデックス後に、ストアレベル属性の一致に基づくカタログ価格ルールが適用されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-43726。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 70e7e1d2-e601-4fed-9274-a1a619de29e1
feature: Catalog Management, Categories, Orders, Price Rules
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# MDVA-43726：部分的な再インデックス後にカタログ価格ルールが適用されない

MDVA-43726 パッチは、部分的な再インデックス後に、ストアレベル属性の一致に基づくカタログ価格ルールが適用されない問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-43726。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

部分的な再インデックス後に、ストアレベル属性の一致に基づくカタログ価格ルールが適用されない。

<u>再現手順</u>:

1. インデクサーモードをスケジュールどおりに実行するように設定します。
1. 設定可能な 2 つの製品属性を作成します。 例：カラー（ビジュアルスウォッチ）およびサイズ（テキストスウォッチ）。
1. 手順 2 で作成した両方の属性を使用して、設定可能な製品を作成します。
1. 商品を作成したら、次を作成します **はい/いいえ** 「attribute」と入力し、ルール条件で表示できるようにします。
1. この属性をデフォルトの属性セットに追加します。
1. この属性が次のように設定されたときに適用するカタログ価格ルールを作成します **はい**.
1. 設定可能な商品に関連するシンプルな商品の 1 つを開きます。
1. 範囲をストア表示に変更し、属性値をに更新します。 **はい**.
1. を実行 `CRON` フロントエンドの価格を確認してください。
1. 完全な再インデックスを実行します。 もう一度、フロントエンドの価格を確認してください。
1. 設定可能な製品カテゴリを更新します。
1. を実行 `CRON` そして、フロントエンドでもう一度価格を確認します。

<u>期待される結果</u>:

増分インデクサーを使用した完全な再インデックスを実行しない場合、カタログルールは正しく適用されます。

<u>実際の結果</u>:

完全な再インデックスを実行しないと、カタログルールは適用されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
