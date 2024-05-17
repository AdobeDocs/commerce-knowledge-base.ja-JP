---
title: 「MDVA-13203 パッチ：503 エラーホームページが完全な再インデックスを投稿」
description: '「MDVA-13203 Adobe Commerce パッチを適用すると、サイトでメンテナンスページが表示され、「system.log」に*CRITICAL: SQLSTATE\[23000\]: Integrity constraint violation*というエラーが記録される問題が修正されます。」 パッチ ID は MDVA-13203。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.13 がインストールされている場合に利用できます。'
exl-id: 8e09010b-9aa4-4a79-b546-a24bb72e0e40
feature: Tools and External Services
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# MDVA-13203 パッチ：503 error homepage post full reindex

MDVA-13203 Adobe Commerce パッチは、サイトにメンテナンスページが表示され、次のような問題を修正します *重大：SQLSTATE\[23000\]：整合性制約違反* のエラー `system.log`. パッチ ID は MDVA-13203。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.13 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.2.4 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce（すべてのデプロイメント方法） 2.3.0～2.4.1。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順：</u>

1. 影響を受ける URL に移動します。
1. メンテナンスページが表示されます。
1. サイトが SSH 経由でメンテナンスステータスになっていないことを確認します。
   <pre> bin/magento メンテナンス：ステータス：メンテナンスモードがアクティブではありません除外 IP アドレスのリスト：なし</pre>
1. を見る `system.log`:

<pre>grep critical -i var/log/system.log |テール [2018-09-04 17:05:18] report.CRITICAL: SQLSTATE[23000]：整合性制約違反：1062 キー'プライマリ'の重複エントリ '4613'、クエリは：INSERT INTO 'search_tmp_5b8ebb4e994da5_88027289' （'entity_id','score'） VALUES （?, ?）,... （?, ?）, （?, ?） [] [] [2018-09-04 17:05:21] report.CRITICAL: SQLSTATE[23000]：整合性制約違反：1062 キー'プライマリ'の重複エントリ '4613'、クエリは：INSERT INTO 'search_tmp_5b8ebb51579943_52333638' （'entity_id','score'） VALUES （?, ?）,...,（?, ?） [] [] [2018-09-04 17:05:47] report.CRITICAL: SQLSTATE[23000]：整合性制約違反：1062 キー'プライマリ'の重複エントリ '1350'、クエリ : INSERT INTO 'search_tmp_5b8ebb6b7028f4_68065024' （'entity_id','score'） VALUES （?, ?）, （?, ?）, （?, ?）, （?, ?）, （?, ?）, （?, ?）, （?, ?）、（?、?）、（?、?）、（?、?）、（?、?）、（?、?） [] [] [2018-09-04 17:05:47] report.CRITICAL: SQLSTATE[23000]：整合性制約違反：1062 キー'プライマリ'の重複エントリ '1350'、クエリ : INSERT INTO 'search_tmp_5b8ebb6b7885a9_23360993' （'entity_id','score'） VALUES （?,?）, （?, ?）, （?, ?）, （?, ?）, （?, ?）, （?, ?）, （?, ?）、（?、?）、（?、?）、（?、?）、（?、?）、（?、?） [] [] 日 9 月 4 日（火） 17:06:11 UTC 2018</pre>

<u>期待される結果：</u> サイトが表示されます。

<u>実際の結果：</u> データベースの一貫性に関する問題が原因で、メンテナンスページに表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
