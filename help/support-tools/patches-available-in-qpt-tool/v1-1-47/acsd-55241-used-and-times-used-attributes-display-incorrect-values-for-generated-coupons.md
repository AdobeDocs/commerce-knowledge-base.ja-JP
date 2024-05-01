---
title: 「ACSD-55241:**使用中**および**使用回数**属性に、生成されたクーポンの誤った値が表示される」
description: ACSD-55241 パッチを適用すると、**Used**属性と**Times Used**属性で生成されたクーポンの値が正しく表示されないAdobe Commerceの問題が修正されます
feature: Price Rules
role: Admin, Developer
exl-id: cfe0f8af-423a-4e12-a332-053392cbabed
source-git-commit: 5d0b4743fe49d22c099102490f93dc4065ab4413
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# ACSD-55241: **使用済み** および **使用回数** 属性に表示されるクーポンの値が正しくない

ACSD-55241 パッチは、 **使用済み** および **使用回数** 属性に表示されるクーポンの値が正しくない。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.47 がインストールされています。 パッチ ID は ACSD-55241 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

**使用済み** および **使用回数** 属性に表示されるクーポンの値が正しくない。

<u>再現手順</u>:

1. 作成 **[!UICONTROL Cart Price Rules]** から **[!UICONTROL Admin]** > **[!UICONTROL Marketing]** > **[!UICONTROL Promotion]** 注文の際に一致する条件を追加します（例：よりも大きい小計） *5$*）

* 割引を適用します。
* を選択 **[!UICONTROL Auto Coupon]**.
* からクーポンコードをいくつか生成します **クーポンコードの管理**.
* キャッシュの再インデックスとクリーンアップを行います。

1. を作成 **[!UICONTROL customer account]** フロントエンドにログインします。
1. 複数のを含む 1 つの製品を追加 *2* 買い物かごの数量を入力し、1 つのクーポンを適用します。
1. クリックする **[!UICONTROL Check Out with Multiple Addresses]**.
1. 数量ごとに個別の所在地を選択し、発注して精算プロセスを完了します。
1. 管理者から注文の合計を確認し、適用された割引を確認します。
1. 別のクーポンで別の注文を行います。
1. を実行 `php81 bin/Magento queue:consumers: start sales.rule.update.coupon.usage &` クーポン コードの使用状況を更新するコマンドです。

<u>期待される結果</u>:

に正しい数が表示されます。 **使用時間** および **使用済み** を含む列 **はい** の値 **[!UICONTROL manage coupon]** が含まれる **[!UICONTROL cart price rule]** admin.

<u>実際の結果</u>:

使用されたクーポンコード数がで更新されません **使用時間** クーポングリッドの列、および **使用済み** 列には *不可* 複数の配送先住所で注文する場合の値。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
