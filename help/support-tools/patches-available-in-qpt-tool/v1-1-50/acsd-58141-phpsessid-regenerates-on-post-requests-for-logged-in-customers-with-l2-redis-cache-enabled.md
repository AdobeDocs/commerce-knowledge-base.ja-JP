---
title: 「ACSD-58141:L2 Redis キャッシュが有効なログイン済みユーザーのPOSTリクエストで PHPSESSID が再生成される」
description: ACSD-58141 パッチを適用すると、L2 Redis キャッシュが有効なログイン済みのお客様のストアフロント領域で、「PHPSESSID」がPOSTリクエストで再生成され、お客様が管理者から更新されるAdobe Commerceの問題を修正できます。
feature: Customers, Cache
role: Admin, Developer
source-git-commit: 488699c5d880baee2f7191d963368415f90c3340
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# ACSD-58141: L2 Redis キャッシュが有効な場合、ログインしている顧客の [!DNL POST] リクエストで PHPSESSID が再生成されます

ACSD-58141 パッチは、L2 Redis キャッシュが有効で、管理者から更新され `PHPSESSID` 場合、ログイン中のお客様の [!DNL POST] リクエストに対して ACSD が再生成する問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.50 がインストールされている場合に使用できます。 パッチ ID は ACSD-58141 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe CommerceおよびMagento Open Sourceバージョンと互換性あり：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p7

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`PHPSESSID` は、L2 Redis キャッシュが有効なログイン済みのお客様の [!DNL POST] リクエストに対して再生成します。

<u> 前提条件 </u>

環境は、少なくとも 3 つのノードを持つ Redis で設定する必要があります。

<u> 再現手順 </u>:

1. シンプルな製品を作成します。
1. 顧客を作成し、ストアフロントにログインします。
1. `PHPSESSID` の値を確認します。
1. [!DNL POST] リクエストをいくつか送信し（例えば、買い物かごに製品を追加するなど）、`PHPSESSID` が同じままであることを確認します。
1. **[!UICONTROL Admin]** パネルにログインし、顧客のミドルネームを変更します。
1. ミドルネームを保存したら、名前を変更して数回保存し直します。
1. ストアフロントで、[!DNL POST] リクエストを送信します。 `PHPSESSID` を更新する必要があります。
1. ストアフロントで別の [!DNL POST] リクエストを送信し、`PHPSESSID` れを確認します。
1. 前の手順を数回繰り返します。

<u> 期待される結果 </u>

`PHPSESSID` は、顧客データを変更した後に 1 回だけ再生成されます。

<u> 実際の結果 </u>:

[!DNL POST] リクエストが送信されるたびに、`PHPSESSID` が再生成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
