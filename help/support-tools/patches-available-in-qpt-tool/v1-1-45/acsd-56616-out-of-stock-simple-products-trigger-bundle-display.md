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

ACSD-56616 パッチは、関連するすべてのシンプルな製品の在庫が切れた場合に、バンドルされた製品がストアフロントに予期せず表示される問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされています。 パッチ ID は ACSD-56616 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

単純な在庫不足の際に、バンドルされた製品の誤ったストアフロント表示が発生する。

<u>再現手順</u>:

1. 新しい web サイト / ストア / ストアフロントを作成します。
1. 新規ソースを作成します。
1. 新しい在庫を作成し、新しく作成した web サイトに割り当てます。
1. スケジュールに従って更新するようにインデクサーを設定します。
1. S1 （数量= 1）と S2 （数量= 1）という 2 つのシンプルな製品を生成して、それらを新しい在庫と新しい web サイトに割り当てます。
1. 作成 *bundled1* 製品を新しい web サイトに関連付けて、カテゴリに配置します *CAT*.
1. 2 つの必須のドロップダウンオプションを定義して、シンプルな製品をリンクします *S1* を option1 へ、を option1 へ *S2* をオプション 2 に変更します。
1. 商品を保存します。
1. に移動します。 **[!UICONTROL System]** > **[!UICONTROL Configuration]** > **[!UICONTROL General]** > **[!UICONTROL Web]** および有効化 *URL にストアコードを追加* = *はい*.
1. ストアフロントを開き、バンドルされた製品を購入します。
1. cron を 2 回実行します。
1. に戻る *CAT* カテゴリ。

<u>期待される結果</u>:

この *bundle1* 製品の在庫がありません。

<u>実際の結果</u>:

この *bundle1* 製品は価格=で表示されます *$0*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
