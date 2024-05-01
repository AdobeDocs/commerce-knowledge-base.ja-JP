---
title: 「MDVA-42326：セッションタイムアウト後、チェックアウト時にエラーが発生する」
description: MDVA-42326 パッチは、永続ショッピング カートが有効になっている場合でも、セッション タイムアウト後にチェックアウト時に顧客にエラーが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.8 がインストールされている場合に利用できます。 パッチ ID は MDVA-42326。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: bc9b71de-510d-4c4e-8b0d-9abf9a3e447f
feature: Checkout, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# MDVA-42326：セッションタイムアウト後、チェックアウト時にエラーが発生する

MDVA-42326 パッチは、永続ショッピング カートが有効になっている場合でも、セッション タイムアウト後にチェックアウト時に顧客にエラーが発生する問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.8 がインストールされています。 パッチ ID は MDVA-42326。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.6 ～ 2.3.7-p2、2.4.1 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

永続買い物かごが有効になっている場合でも、セッションタイムアウト後のチェックアウトでエラーが発生します。

<u>前提条件</u>:

1. に移動 **設定** > **一般** > **Web** > **デフォルトの Cookie 設定** > **Cookie の有効期間** をに設定します。 **120**.
1. に移動 **設定** > **顧客** > **顧客設定** > **オンライン顧客オプション** 両方の値をに設定します。 **2**.
1. に移動 **設定** > **顧客** > **永続ショッピングカート** をに設定します。 **Enable （有効）**.
1. に移動 **設定** > **売上** > **支払い方法** 以外のすべての支払い方法を無効にする **小切手/送金** （有効にする必要があります）。

<u>再現手順</u>:

1. 顧客としてログインし、いくつかの製品を買い物かごに追加します。
1. 買い物かごを確認します。
1. 2 分待ちます（事前条件で設定）。セッションはタイムアウトします。
1. クリック **チェックアウトに移動** ページは更新しないでください。
1. ゲストとしてチェックアウトし、配送先住所を入力して、配送方法を選択します。
1. クリック **次**.
1. 日 **レビューと支払い** ページ、クリック **注文する**. お支払い方法は 1 つのみなので、お客様は支払い方法を選択せずに注文できる必要があります。

<u>期待される結果</u>:

お客様が注文できるはずです。

<u>実際の結果</u>:

お客様に次のエラーが表示される。 *アドレスの検証に失敗しました：電子メールの形式が間違っています*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
