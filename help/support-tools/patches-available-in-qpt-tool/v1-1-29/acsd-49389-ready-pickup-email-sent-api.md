---
title: 「ACSD-49389：受け取りの準備が整っていない場合に API から送信される受け取りの準備ができたメール」
description: ACSD-49389 パッチを適用すると、注文の受け取りの準備が整っていない場合に、API から受け取り準備完了のメールが送信されるAdobe Commerceの問題が修正されます。
exl-id: a1baae06-cf36-448b-bda4-aff1e5ca68db
feature: REST, Communications
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# ACSD-49389：受け取りの準備が整っていない場合に API から送信される受け取りの準備ができたメール

ACSD-49389 パッチは、注文が集荷の準備ができていない場合に、API によって集荷準備完了のメールが送信される問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされています。 パッチ ID は ACSD-49389 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [QPT ランディングページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文が受け取り準備ができていない場合、受け取り準備が整ったメールが API から送信されます。

<u>再現手順</u>:

1. Enable （有効） *[!UICONTROL In-Store Delivery]* メソッド。
1. 集荷場所が有効な在庫ソースを作成します。
1. 上記で作成したソースを使用して、メイン web サイトを使用して新しい在庫を作成します。
1. 同じソースを割り当てる商品を作成します。
1. 在庫数量= 1 を設定します。
1. 手順 4 で作成した製品を、 *[!UICONTROL In-Store Delivery]* ストアフロントからの方法。
1. 注文の請求書を作成します。
1. 製品の数量を次のように設定： *0* 在庫切れにする。
1. 次の API リクエストを投稿します。

```
{
    "orderIds": [
        1
    ]
}
```

<u>期待される結果</u>:

集荷準備完了の E メールは送信されません。

<u>実際の結果</u>:

API の戻り値 *注文の受け取りの準備が整っていません*&#x200B;ただし、集荷準備が完了した電子メールが送信されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
