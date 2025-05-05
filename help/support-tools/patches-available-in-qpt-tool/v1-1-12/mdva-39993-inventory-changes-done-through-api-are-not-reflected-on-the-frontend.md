---
title: 「MDVA-39993:API を使用して行われたインベントリの変更がストアフロントに反映されない」
description: MDVA-39993 パッチは、API を介して行われたインベントリの変更がストアフロントに反映されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-39993。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 2d49b9b7-8a70-44f3-80bf-4460bb2e61d5
feature: REST, Inventory, Orders, Storefront
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# MDVA-39993: API を使用して行われたインベントリの変更がストアフロントに反映されない

MDVA-39993 パッチは、API を介して行われたインベントリの変更がストアフロントに反映されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.12 がインストールされている場合に使用できます。 パッチ ID は MDVA-39993。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.3.7-p2 および 2.4.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

API を通じて行われた在庫の変更は、ストアフロントの製品ページには反映されません。

<u> 前提条件 </u>:

インストール済みのインベントリモジュール。

<u> 再現手順 </u>:

1. キューが cron で実行するように設定され、cron がインストールされ実行中であることを確認します。
1. 2 つの色（黒と赤）、2 つのサイズ（M と L）を持つ設定可能な製品（COC001）を作成します。
1. 在庫切れ（COC001-Red-M）を 1 つ作成します。
1. 設定可能な製品ページをストアフロントに読み込んで、各色をクリックしてみてください。 **赤** をクリックすると、在庫切れのため **M** サイズが消えます。
1. 次の API エンドポイントとペイロードを使用して、COC001-Red-M を在庫にします。

   ```json
   POST http://{domain}/rest/V1/inventory/source-items
   
   {
     "sourceItems": [
       {
         "sku": "COC001-Red-M",
         "source_code": "default",
         "quantity": 1000,
         "status": 1
       }
     ]
   }
   ```

1. バックエンドからこの単純な製品をチェックし、それが In Stock に更新されていることを確認します。
1. フロントエンドから設定可能な製品を読み込み、各色をクリックします。 **赤** をクリックすると、サイズ **M** に注目してください。

<u> 期待される結果 </u>:

API を使用して在庫に更新したので、COC001-Red-M オプションは廃止されません。

<u> 実際の結果 </u>:

COC001-Red-M オプションは、在庫があるにもかかわらず、まだ取り消されています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
