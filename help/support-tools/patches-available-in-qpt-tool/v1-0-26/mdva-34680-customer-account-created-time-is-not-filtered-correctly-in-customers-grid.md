---
title: 「MDVA-34680：顧客グリッドで顧客アカウントが正しくフィルタリングされない」
description: 00:00 UTC の後に作成されたカスタマーアカウントが顧客のグリッドで正しくフィルタリングされていない場合、MDVA-34680 パッチはこの問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.26 がインストールされている場合に利用できます。 パッチ ID は MDVA-34680。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 2e506d7a-8cde-41eb-84b2-1a5ff8015428
feature: Customer Service
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# MDVA-34680：顧客グリッドで顧客アカウントが正しくフィルターされない

00:00 UTC の後に作成されたカスタマーアカウントが顧客のグリッドで正しくフィルタリングされていない場合、MDVA-34680 パッチはこの問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.26 がインストールされている場合に使用できます。 パッチ ID は MDVA-34680。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 および 2.4.2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.6-2.3.7 および 2.4.1-2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

00:00 UTC の後に顧客アカウントが作成され、その日付でアカウントをフィルタリングしようとすると、この顧客は返されません。

<u> 再現手順 </u>:

1. **ストア**/**設定**/**一般** に移動し、「タイムゾーン」を Eastern Standard[ 米国/ニューヨーク ] に設定します。
1. 00:00 UTC の後に新しい顧客アカウントを作成します。
1. **顧客**/**すべての顧客** に移動し、今日の日付でアカウントをフィルタリングします。

<u> 期待される結果 </u>:

顧客アカウントフィルターには、今日 00:00 UTC の後に作成された新しいアカウントが表示されます。

<u> 実際の結果 </u>:

顧客アカウントフィルターには、今日作成された新しいアカウントは表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
