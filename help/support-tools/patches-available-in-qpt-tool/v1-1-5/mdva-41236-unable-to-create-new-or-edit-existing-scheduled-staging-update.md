---
title: 「MDVA-41236：製品の新しいスケジュールされた更新を作成または既存のスケジュールされた更新を編集できない」
description: MDVA-41236 パッチは、「終了日」が既に削除されている場合、ユーザーが製品の新しいスケジュール済み更新を作成したり、既存のスケジュール済み更新を編集したりできない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-41236。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 00d6c0af-f248-49f6-aaa2-3ae3c0294832
feature: Products, Staging
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# MDVA-41236：製品のスケジュールされた更新を新規作成または編集できない

MDVA-41236 パッチは、「終了日」が既に削除されている場合、ユーザーが製品の新しいスケジュール済み更新を作成したり、既存のスケジュール済み更新を編集したりできない問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.1.5 がインストールされています。 パッチ ID は MDVA-41236。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「終了日」が以前に削除されている場合、ユーザーが製品の新しいスケジュールを作成したり、既存のスケジュールを編集したりできない。

<u>再現手順</u>:

1. ステータスがに設定された製品を作成します *disable*.
1. スケジュールされた更新を追加してこの製品を有効にします。
   * 未来の開始日と終了日を追加します。
1. を削除して、スケジュールされた更新を編集 **終了日**.
1. スケジュールを再度編集し、 **終了日**. エラーが発生します。
1. ページを更新して、もう一度に移動します **スケジュールされた更新を編集**.
1. クリック **更新から削除** > **更新を削除**.
1. これで、製品の編集ページの上部にスケジュール済み更新が表示されなくなります。
1. 前の期間と重なる新しいスケジュール済み更新を作成してみてください。

<u>期待される結果</u>:

* 手順 4 でエラーは発生しません。 スケジュールがまだアクティブでないので、管理者はエラーなくスケジュールされた更新を更新できます。
* 管理者ユーザーは、以前の更新を削除して新しい更新を作成できます。

<u>実際の結果</u>:

次のエラーメッセージが表示されます。

*エラー：この時間範囲には今後の更新が既に存在します。 別の範囲を設定して、もう一度試してください。*


## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
