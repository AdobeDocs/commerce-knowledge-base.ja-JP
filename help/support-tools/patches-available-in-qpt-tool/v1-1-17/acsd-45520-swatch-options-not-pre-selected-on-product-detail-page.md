---
title: 「ACSD-45520：製品の詳細ページでスウォッチオプションが選択されない」
description: ACSD-45520 パッチは、ユーザーが買い物かごから設定可能な製品を編集する際に、製品の詳細ページでスウォッチオプションが事前に選択されていない問題を修正しています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.17 がインストールされている場合に利用できます。 パッチ ID は ACSD-45520 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 941f4a45-bc3c-44c0-a582-ddfe179fa8c3
feature: Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# ACSD-45520：製品の詳細ページでスウォッチオプションが選択されない

ACSD-45520 パッチは、ユーザーが買い物かごから設定可能な製品を編集する際に、製品の詳細ページでスウォッチオプションが事前に選択されていない問題を修正しています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.17 がインストールされている場合に使用できます。 パッチ ID は ACSD-45520 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーが買い物かごから設定可能な製品を編集すると、製品の詳細ページでスウォッチオプションが選択されません。

<u> 再現手順 </u>:

1. 商品オプション（色など）を使用して設定可能な商品を作成します。
1. 設定可能な製品を買い物かごに追加します。
1. 自分の買い物かごページに移動します。
1. 手順 1 で追加した設定可能な製品の「編集」ボタンをクリックします。
1. 編集ページの製品オプションを確認します。

<u> 期待される結果 </u>:

製品オプションが選択されます。

<u> 実際の結果 </u>:

製品オプションが選択されていません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
