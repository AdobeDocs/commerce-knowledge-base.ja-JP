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

MDVA-28191 パッチは、ある Web サイトの Admin **Create New Order** で支払い方法が読み込まれない問題を修正します。ただし、他の Web サイトでは支払い方法が表示されることがあります。  このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) ツール バージョン 1.0.5 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.3 から 2.4.1 （2.3.5-p1 を含む）。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

バックエンドから注文を作成する場合、Adobe Commerceは 2 つの見積もりを作成し、1 つは非アクティブで、もう 1 つはアクティブです。 ただし、セッションには非アクティブな Quote ID が保持されます。

<u> 再現手順 </u>

1. **管理パネル**/**営業**/**注文** に移動し、「**新規注文を作成**」ボタンをクリックします。
1. 注文を作成する顧客を選択します。
1. ストアに複数のビューがある場合は、選択したユーザーの **新しい注文を作成** ページで、注文を送信するストアのビューを選択します。
1. 「**顧客のアクティビティ**」セクションから、または **製品を追加** をクリックしてカタログから製品を追加します。 ページを下にスクロールして、注文の必要に応じて次のセクションを完了します。
   * クーポンコードの適用
   * 支払い方法
   * 発送方法
   * 注文コメント

<u> 期待される結果：</u>

すべての web サイトに対して、管理者で支払い方法を読み込む必要があります。

<u> 実際の結果：</u>

本ウェブサイトでは、お支払い方法が利用できません（*お支払い情報が必要ありません*」というメッセージも表示されません）。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
