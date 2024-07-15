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

MDVA-35092 パッチを適用すると、「*&quot;Video not Found&quot;*」というエラーが表示される問題が修正されます。 このエラーメッセージが表示されるのは、Adobe Commerceの製品管理で、ネイティブのビデオを追加インターフェイスを使用して Vimeo ビデオにアクセスした場合です。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.17 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.5 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Vimeo simple API が正常に動作しなくなります。

<u> 再現手順 </u>:

1. 管理者にログインします。
1. 既存の製品を編集するには、**カタログ**/**製品**/**編集** に移動します。また、新しい製品を作成するには、**カタログ**/**製品**/**編集**/**製品を追加** に移動します。
1. 製品ページの「**画像とビデオ**」タブをクリックします。
1. **動画を追加** をクリックし、Vimeo 動画の URL を追加します。 **保存** をクリックします。

<u> 期待される結果 </u>:

新しいビデオが見つかり、保存されます。

<u> 実際の結果 </u>:

エラー：「*ビデオが見つかりません」* が表示される。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
