---
title: 「MDVA-36464：送信メールの設定がストア表示レベルで機能しない」
description: MDVA-36464 パッチでは、送信メールの設定がストアビューレベルで機能しない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.21 がインストールされている場合に利用できます。 パッチ ID は MDVA-36464。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: cdf7e208-90ee-4711-8407-026da42fe3c8
feature: Communications
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# MDVA-36464：送信メールの設定がストア表示レベルで機能しない

MDVA-36464 パッチでは、送信メールの設定がストアビューレベルで機能しない問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.21 がインストールされています。 パッチ ID は MDVA-36464。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.4.0-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>前提条件：</u>

クリーンなAdobe Commerceをインストールします。

<u>再現手順</u>:

1. 追加の web サイト、ストア、ストア表示を作成します（この例では、2 番目の web サイトはです）。 *website2*）に設定します。
1. 無効 **メール通知** ～の世界レベルで **ストア** > **設定** > **詳細** > **システム** > **メール送信設定**.
1. Enable （有効） **メール通知** 日 *website2* レベル （**メール通信を無効にする** = *不可*）に設定します。
1. 管理者で、新しいユーザーを作成し、に割り当てます *website2*.
1. 管理者の顧客の編集ページで、 **パスワードをリセット** （上記で手順 4 で作成した顧客の場合）。

<u>期待される結果</u>:

両方 **お知らせメール** および **パスワードリセットメール** は、以下の理由から、期待どおりに送信されます **メール通信を無効にする** = *不可* 2 つ目の web サイトの場合（例： *website2*）に設定します。

<u>実際の結果</u>:

* この **お知らせメール** 新規顧客の作成後は、トリガーされません。
* この **パスワードリセットメール** がトリガーされない。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
