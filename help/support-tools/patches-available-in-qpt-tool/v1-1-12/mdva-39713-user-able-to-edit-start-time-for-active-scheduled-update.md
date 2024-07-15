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

MDVA-39713 パッチは、ユーザーがアクティブなスケジュールされた更新の開始時刻を編集できる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.12 がインストールされている場合に使用できます。 パッチ ID は MDVA-39713。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.6

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーは、スケジュールされたアクティブな更新の開始時刻を編集できます。

<u> 再現手順 </u>:

1. 新しい CMS ページを作成します。
1. **新規更新をスケジュール** を選択し、**開始日** を現在の+1 分に設定します。
1. ローカル環境でコマンド `bin/magento cron:run --group=staging` を実行して、スケジュールされたアップデートをアクティベートします。 数分待ってから、スケジュールがアクティブかどうかを確認します。
1. スケジュールがアクティブになったら、ページを更新します。
1. 「スケジュールされた変更」セクションの「**表示/編集**」をクリックします。
1. +2 分を追加して時間を編集し、変更を保存します。
1. CMS ページを保存します。
1. 再び、次のコマンドを実行します：`bin/magento cron:run --group=staging`。
1. スケジュールされている更新の **表示/編集** をクリックします。

<u> 期待される結果 </u>:

ユーザーは、スケジュールされたアクティブな更新の開始時刻を編集できません。

<u> 実際の結果 </u>:

同じ ID 「11」の *Item （Magento\Cms\Model\Page） already exists* のようなエラーがユーザーに表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
