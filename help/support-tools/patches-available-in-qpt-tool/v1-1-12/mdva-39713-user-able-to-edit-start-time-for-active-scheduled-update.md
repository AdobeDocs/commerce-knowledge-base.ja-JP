---
title: 「MDVA-39713：ユーザーは、アクティブなスケジュールされた更新の開始時刻を編集できる」
description: MDVA-39713 パッチは、ユーザーがアクティブなスケジュールされた更新の開始時刻を編集できる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-39713。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: c7221fdb-5fc0-4179-8d4c-c9e1f0d00692
feature: CMS
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# MDVA-39713: ユーザーは、アクティブなスケジュールされた更新の開始時刻を編集できます

MDVA-39713 パッチは、ユーザーがアクティブなスケジュールされた更新の開始時刻を編集できる問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-39713。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.6

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーは、スケジュールされたアクティブな更新の開始時刻を編集できます。

<u>再現手順</u>:

1. 新しい CMS ページを作成します。
1. を選択 **新しい更新をスケジュール** を設定して、 **開始日** を現在の+1 分に変更します。
1. コマンドを実行して、スケジュールされた更新をアクティベートします。 `bin/magento cron:run --group=staging` ローカル環境で。 数分待ってから、スケジュールがアクティブかどうかを確認します。
1. スケジュールがアクティブになったら、ページを更新します。
1. クリック **表示/編集** 「スケジュールされた変更」セクションで、次の操作を行います。
1. +2 分を追加して時間を編集し、変更を保存します。
1. CMS ページを保存します。
1. 再び、次のコマンドを実行します。 `bin/magento cron:run --group=staging`.
1. クリック **表示/編集** （スケジュールされた更新）。

<u>期待される結果</u>:

ユーザーは、スケジュールされたアクティブな更新の開始時刻を編集できません。

<u>実際の結果</u>:

ユーザーに次のようなエラーが表示されます *同じ ID を持つ項目（Magento\Cms\Model\Page）が既に存在しています。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
