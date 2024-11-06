---
title: 「MDVA-37115:「Only 0 left」の通知が製品ページに表示される」
description: MDVA-37115 パッチを適用すると、設定可能な製品ページに不要な*Only 0 left*通知が表示される問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-37115。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 08aa6ac7-13ae-44c1-9db4-d449c3d8c985
feature: Configuration, Products, Orders
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# MDVA-37115：製品ページに「Only 0 left」の通知が表示される

MDVA-37115 パッチにより、設定可能な製品ページに不要な *残り 0 のみ* 通知が表示される問題が解決されました。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.2 がインストールされている場合に使用できます。 パッチ ID は MDVA-37115。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメントタイプ） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメントタイプ） 2.4.2 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な製品ページに、不要な *左側が 0 のみ* 通知が表示されます。

<u> 前提条件 </u>:

インベントリモジュールがインストールされます。

<u> 再現手順 </u>:

1. オプションが少ない設定可能な製品を作成します。
1. フロントエンドに移動します。
1. 設定可能な製品ページを開き、任意のオプションを選択します。

<u> 期待される結果 </u>:

製品ページに *残り 0 のみ* の表示はありません。

<u> 実際の結果 </u>:

*残り 0 件のみ* が製品ページに表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
