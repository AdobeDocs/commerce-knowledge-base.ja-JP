---
title: 「MDVA-37725：デフォルト以外のサイトを介して送信されるメールには、デフォルトのサイトのロゴ URL が含まれる」
description: MDVA-37725 パッチは、デフォルト web サイトのロゴ URL を含むデフォルト以外の web サイトから非同期注文 E メールが送信される問題を修正します。
exl-id: c0d1b9a3-01bb-445b-b7da-f9be6952eaeb
feature: Communications, Orders
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# MDVA-37725：デフォルト以外のサイトを介して送信されるメールには、デフォルトのサイトのロゴ URL が含まれる

>[!WARNING]
>
> MDVA-37725 パッチは非推奨（廃止予定）です。

MDVA-37725 パッチは、デフォルト web サイトのロゴ URL を含むデフォルト以外の web サイトから非同期注文 E メールが送信される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/patches/overview)1.1.4 がインストールされている場合に使用できます。 パッチ ID は MDVA-37725。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

非同期注文メールは、デフォルト Web サイトのロゴ URL を含んだデフォルト以外の Web サイトから送信されます。

<u> 前提条件 </u>:

1. 2 つ目の web サイト/ストア/ストアビューを作成する必要があります。
1. **非同期送信** 設定は、**Stores**/**Settings**/**Configuration**/**Sales**/**Sales Email**/**General Settings** から有効にする必要があります。
1. **URL へのストアコードの追加** セカンダリ Web サイトへのアクセスを容易にするため、設定を **ストア**/**設定**/**設定**/**URL オプション** からオンにします。

<u> 再現手順 </u>:

1. 1 号店と 2 号店の両方から注文します。
1. cron を実行して販売メールを送信します。
1. 2 番目の web サイトからメールを確認します。

<u> 期待される結果 </u>:

メールのロゴ URL には、2 番目の web サイトの URL が含まれます。

<u> 実際の結果 </u>:

メールのロゴ URL には、デフォルトの web サイトの URL が含まれます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
