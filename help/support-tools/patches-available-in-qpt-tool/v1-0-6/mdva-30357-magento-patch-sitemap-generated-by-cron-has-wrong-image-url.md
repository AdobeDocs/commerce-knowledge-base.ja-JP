---
title: 「MDVA-30357:cron によって生成されたサイトマップの画像 URL が間違っている」
description: MDVA-30357 パッチは、Commerce Admin で cron 生成のサイトマップによって間違った画像 URL が作成される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.6 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: c91f7ae0-0970-4918-9d1f-4ede6bfcb05f
feature: Marketing Tools
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# MDVA-30357: cron によって生成されたサイトマップに間違った画像 URL がある

MDVA-30357 パッチは、Commerce Admin で cron 生成のサイトマップによって間違った画像 URL が作成される問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.6 がインストールされています。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 から 2.4.0

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Adobe Commerceの cron で生成されたサイトマップに間違った画像 URL パスが含まれている。

<u>再現手順</u>:

1. Commerce管理者で、新しい web サイト、ストアまたはストアビューを作成します。
1. 各店舗に 1 つ以上の製品を追加し、各製品に 1 つ以上の画像を追加します。
1. Enable （有効） **スケジュールによるサイトマップの生成** 。対象： **Admin** > **ストア** > **設定** > **カタログ** > **XML サイトマップ** > **生成設定**.
1. 2 つのストアのいずれかについて、で手動でサイトマップを生成する **Admin** > **Marketing** > **サイトマップ** 「」のようなサイトマップ名を使用します&#x200B;*sitemap.xml*」と入力します。
   * ファイル名を「」に変更します&#x200B;*manual\_sitemap.xml*」を選択するか、ファイルコンテンツを任意のテキストエディターにコピーします。
1. cron ジョブによる同じサイトマップの生成 `sitemap_generate`.
1. 手動で生成されたサイトマップを比較&#x200B;*manual\_sitemap.xml*」と、cron によって生成されたサイトマップ。*sitemap.xml*」と入力します。

<u>期待される結果</u>:

キャッシュされたサイトマップ画像パスの URL が正しいです。

<u>実際の結果</u>:

cron によって生成されたサイトマップに間違った画像パス URL が含まれている。 から画像を開こうとした場合&#x200B;*sitemap.xml*」が表示されます。デフォルトのプレースホルダーが表示されます。 手動で生成されたサイトマップ URL は、この問題の影響を受けません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。

サイトマップについて詳しくは、開発者向けドキュメントで次の記事を参照してください。

* [サイトマップと検索エンジンロボットの追加](https://devdocs.magento.com/cloud/trouble/robots-sitemap.html)
* [Cron の設定と実行](https://devdocs.magento.com/guides/v2.4/config-guide/cli/config-cli-subcommands-cron.html)
* [ブラウザーで実行する cron.php を保護する](https://devdocs.magento.com/guides/v2.4/config-guide/secy/secy-cron.html)
