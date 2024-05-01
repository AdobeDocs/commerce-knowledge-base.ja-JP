---
title: 「MDVA-28191:Admin Create New Order で 1 つの Web サイトに支払い方法がありません」
description: MDVA-28191 パッチは、ある Web サイトの管理者**新しい注文を作成**で支払い方法が読み込まれない問題を修正します。ただし、他の Web サイトでは支払い方法が表示される場合があります。  このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） ツール バージョン 1.0.5 がインストールされている場合に使用できます。
exl-id: 42169743-4f09-4f0a-aadd-931cccc9b467
feature: Admin Workspace, Orders, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# MDVA-28191: Admin Create New Order で 1 つのウェブサイトに支払い方法がありません

MDVA-28191 パッチを適用すると、管理者に支払い方法が読み込まれない問題が修正されます **新しい注文を作成** 1 つの web サイトの場合は、他の web サイトの場合でも支払い方法が表示されることがあります。  このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) ツール バージョン 1.0.5 がインストールされています。

## 影響を受ける製品とバージョン

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.3 から 2.4.1 （2.3.5-p1 を含む）。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

バックエンドから注文を作成する場合、Adobe Commerceは 2 つの見積もりを作成し、1 つは非アクティブで、もう 1 つはアクティブです。 ただし、セッションには非アクティブな Quote ID が保持されます。

<u>再現手順</u>

1. に移動 **管理パネル** > **売上** > **注文件数** をクリックし、 **新しい注文を作成** ボタン。
1. 注文を作成する顧客を選択します。
1. ストアに複数のビューがある場合は、注文を行うストアのビューを **新しい注文を作成** 選択したユーザーのページ。
1. からの製品の追加 **顧客のアクティビティ** をクリックしてカタログから選択または削除 **製品を追加**. ページを下にスクロールして、注文の必要に応じて次のセクションを完了します。
   * クーポンコードの適用
   * 支払い方法
   * 発送方法
   * 注文コメント

<u>期待される結果：</u>

すべての web サイトに対して、管理者で支払い方法を読み込む必要があります。

<u>実際の結果：</u>

支払い方法が利用できません（メッセージ「」も同様です）*お支払い情報は不要です*）で表示されます。ただし、他の web サイトの注文をテストする際に支払い方法が表示される場合があります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
