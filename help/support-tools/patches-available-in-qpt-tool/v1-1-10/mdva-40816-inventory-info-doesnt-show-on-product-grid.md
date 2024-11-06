---
title: 「MDVA-40816：在庫データが製品グリッドに表示されない」
description: MDVA-40816 パッチは、製品 SKU に特殊文字が含まれている場合に、製品グリッドに在庫情報が表示されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.10 がインストールされている場合に利用できます。 パッチ ID は MDVA-40816。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 88c05c88-33be-4d72-a302-23a1510c401c
feature: Admin Workspace, Inventory, Orders, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# MDVA-40816：在庫データが製品グリッドに表示されない

MDVA-40816 パッチは、製品 SKU に特殊文字が含まれている場合に、製品グリッドに在庫情報が表示されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.10 がインストールされている場合に使用できます。 パッチ ID は MDVA-40816。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

商品 SKU に特殊シンボルが含まれている場合、在庫データは商品グリッドに表示されません。

<u> 前提条件 </u>:

MSI がインストールされます。

<u> 再現手順 </u>:

1. シンプルな製品を作成します。
1. 製品の SKU を変更して&amp;、&#39;などの特殊シンボルを含めます。
1. 製品グリッドを開きます。

<u> 期待される結果 </u>:

製品グリッドには、すべての情報が正しく表示されます。

<u> 実際の結果 </u>:

在庫データがありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
