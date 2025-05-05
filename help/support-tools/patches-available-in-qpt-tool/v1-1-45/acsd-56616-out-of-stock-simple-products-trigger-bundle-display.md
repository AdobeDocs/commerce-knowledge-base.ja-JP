---
title: 「ACSD-56616 在庫切れ時のセット商品の店頭ディスプレイ」
description: ACSD-56616 パッチを適用すると、関連するすべてのシンプルな商品の在庫切れ時に、バンドルされた商品が予期せずストアフロントに表示されるAdobe Commerceの問題を修正できます。
feature: Products
role: Admin, Developer
exl-id: 6cf8e15d-38a5-42b6-aee7-67410b501404
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# ACSD-56616: シンプルな在庫不足の際にバンドルされた製品の店頭ディスプレイ。

ACSD-56616 パッチは、関連するすべてのシンプルな製品の在庫が切れた場合に、バンドルされた製品がストアフロントに予期せず表示される問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされている場合に使用できます。 パッチ ID は ACSD-56616 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

単純な在庫不足の際に、バンドルされた製品の誤ったストアフロント表示が発生する。

<u> 再現手順 </u>:

1. 新しい web サイト / ストア / ストアフロントを作成します。
1. 新規ソースを作成します。
1. 新しい在庫を作成し、新しく作成した web サイトに割り当てます。
1. スケジュールに従って更新するようにインデクサーを設定します。
1. S1 （数量= 1）と S2 （数量= 1）という 2 つのシンプルな製品を生成して、それらを新しい在庫と新しい web サイトに割り当てます。
1. *bundled1* 製品を作成して新しい web サイトに関連付け、カテゴリ *CAT* に配置します。
1. 2 つの必須ドロップダウンオプションを定義して、単純な製品 *S1* を option1 にリンクし、*S2* を option2 にリンクします。
1. 商品を保存します。
1. **[!UICONTROL System]**/**[!UICONTROL Configuration]**/**[!UICONTROL General]**/**[!UICONTROL Web]** に移動し、「*URL にストアコードを追加* = *はい* を有効にします。
1. ストアフロントを開き、バンドルされた製品を購入します。
1. cron を 2 回実行します。
1. *CAT* カテゴリに戻ります。

<u> 期待される結果 </u>:

*bundle1* 製品の在庫切れです。

<u> 実際の結果 </u>:

*bundle1* 製品が、価格= *$0* で表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
