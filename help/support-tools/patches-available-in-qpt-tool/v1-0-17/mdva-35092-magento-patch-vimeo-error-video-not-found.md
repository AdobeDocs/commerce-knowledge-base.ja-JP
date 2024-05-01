---
title: 「MDVA-35092:Vimeo エラー：「ビデオが見つかりません」」
description: 「MDVA-35092 パッチを適用すると、次のエラーが表示される問題が修正されます。*"Video not Found"* このエラーメッセージが表示されるのは、Adobe Commerceの製品管理で、ネイティブのビデオを追加インターフェイスを使用して Vimeo ビデオにアクセスした場合です。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.17 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.3 で修正されました。'
exl-id: bc0952d9-1ea4-417c-926c-96875984d82c
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# MDVA-35092:Vimeo エラー：「ビデオが見つかりません」

MDVA-35092 パッチを適用すると、次のエラーが表示される問題が修正されます。 *「ビデオが見つかりません」*. このエラーメッセージが表示されるのは、Adobe Commerceの製品管理で、ネイティブのビデオを追加インターフェイスを使用して Vimeo ビデオにアクセスした場合です。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.17 がインストールされています。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.5 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Vimeo simple API が正常に動作しなくなります。

<u>再現手順</u>:

1. 管理者にログインします。
1. 既存の製品を編集するには、に移動してください。 **カタログ** > **製品** > **編集**&#x200B;または、新しい製品を作成するには、に移動してください。 **カタログ** > **製品** > **編集** > **製品を追加**.
1. 「」をクリックします **画像とビデオ** 製品ページの「」タブ。
1. クリック **ビデオを追加** Vimeo 動画の URL を追加します。 クリック **保存**.

<u>期待される結果</u>:

新しいビデオが見つかり、保存されます。

<u>実際の結果</u>:

エラー： *「ビデオが見つかりません」* が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
