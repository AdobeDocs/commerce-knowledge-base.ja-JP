---
title: 「MDVA-42584：設定可能な製品の在庫ステータスが自動的に更新されない」
description: MDVA-42584 パッチは、シンプルな製品が更新されても、設定可能な製品の在庫ステータスが自動的に更新されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.10 がインストールされている場合に利用できます。 パッチ ID は MDVA-42584。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: bf2697a2-8d15-408b-8d59-7b4173537e60
feature: Configuration, Orders, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# MDVA-42584：設定可能な商品の在庫ステータスが自動的に更新されない

MDVA-42584 パッチは、シンプルな製品が更新されても、設定可能な製品の在庫ステータスが自動的に更新されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.10 がインストールされている場合に使用できます。 パッチ ID は MDVA-42584。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

API または読み込みを通じてシンプルな製品が **在庫中** に設定されている場合、バックエンドの設定可能な製品の在庫ステータスは自動的には更新されません。

<u> 前提条件 </u>:

MSI がインストールされました。

<u> 再現手順 </u>:

1. 設定可能な製品 **InvCheck001** を作成します。その際、**InvCheck001-M** と **InvCheck001-L** の 2 つのオプションを使用します。
1. シンプルな製品は両方とも数量が必要で、設定可能な製品もバックエンドでは **在庫** となるように、数量 **在庫** にする必要があります。
1. ここでは、シンプルな製品を更新し、数量を **0** に、在庫ステータスを **在庫切れ** に設定します。
1. 設定可能な商品を更新し、在庫ステータスが「在庫切れ **に更新されていることを確認し** す。
1. 次の API エンドポイントを使用し、シンプルな製品 **InvCheck001-M** を **在庫** に設定して、数量を 0 より大きくします。

   ```JSON
   /rest/V1/inventory/source-items
   
   {
     "sourceItems":
     [
       {
         "sku": "InvCheck001-M",
         "source_code": "default",
         "quantity": 10,
         "status": 1
       }
     ]
   }
   ```

1. バックエンドに移動し、シンプルな製品 **InvCheck001-M** の数量と在庫状況を確認します。 「在庫あり **に更新されま**。
1. 設定可能な製品を更新し、在庫ステータスを確認します。

<u> 期待される結果 </u>:

バックエンドの設定可能な商品 **InvCheck001** の在庫ステータスは、自動的に **在庫中** に更新されます。

<u> 実際の結果 </u>:

設定可能な商品の在庫ステータスは、まだ **在庫切れ** です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
