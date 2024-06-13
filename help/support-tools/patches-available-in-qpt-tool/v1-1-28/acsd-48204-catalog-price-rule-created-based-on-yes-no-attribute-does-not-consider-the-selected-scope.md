---
title: 「ACSD-48204:*Yes/No*属性に基づいて作成されたカタログ価格ルールで、選択した範囲が考慮されない」
description: ACSD-48204 パッチを適用すると、*Yes/No*属性に基づいて作成されたカタログ価格ルールが選択した範囲を考慮しないAdobe Commerceの問題が修正されます。
exl-id: 9b0b4d62-c4c5-40d7-a279-52f59ee7ac42
feature: Admin Workspace, Attributes, Catalog Management, Orders, Price Rules
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# ACSD-48204: カタログ価格ルールは次に基づいて作成されました *はい/いいえ* 属性は選択された範囲を考慮しません

ACSD-48204 パッチは、カタログ価格ルールが基づいて作成された問題を修正します *はい/いいえ* 属性は選択されたスコープを考慮しません。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされています。 パッチ ID は ACSD-48204 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カタログ価格ルールの作成基準 *はい/いいえ* 属性は選択されたスコープを考慮しません。

<u>再現手順</u>:

1. 2 つの web サイト（デフォルトと W2）を作成します。
1. 次の製品属性を作成 *はい/いいえ* タイプ。
   * を設定 [!UICONTROL Default value] = [!UICONTROL No]
   * [!UICONTROL Scope] = [!UICONTROL Website]
   * [!UICONTROL Use for Promo Rule Conditions] = [!UICONTROL Yes]
1. 2 つのバリエーション（V1 と V2）を持つ任意の属性に基づいて、設定可能な製品を作成します。
   * を追加 *はい/いいえ* 設定可能なバリエーション属性セットの属性
   * バリエーション（V1）の 1 つに対して、値をに設定します *[!UICONTROL Yes]* デフォルト以外の web サイト（W2）
1. カタログルールを作成します。
   * 両方の web サイトに適用
   * 条件： *はい/いいえ* 属性値は *[!UICONTROL Yes]*
   * 割引= 50%
1. 設定可能な製品を非デフォルト web サイト（W2）で開きます。
1. V1 バリエーションに 50% のディスカウントが適用されていることを確認します。
1. Adobe Commerce Admin で V1 バリエーションを開きます。
   * デフォルトの Web サイトに切り替える
   * 何も変更せず、商品を保存する
1. 設定可能な製品ストアフロントページを更新します。

<u>期待される結果</u>:

V1 バリエーションには、変更が行われていないので、引き続き 50% のディスカウントが適用されます。

<u>実際の結果</u>:

割引が消える。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
