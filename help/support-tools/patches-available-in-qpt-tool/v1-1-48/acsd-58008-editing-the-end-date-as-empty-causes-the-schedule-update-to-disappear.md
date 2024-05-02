---
title: 「ACSD-58008：終了日を*空*として編集すると、スケジュールの更新が表示されない」
description: ACSD-58008 パッチを適用して、終了日を*空*に変更するとスケジュールの更新が消えるAdobe Commerceの問題を修正してください。
feature: Staging, Page Content
role: Admin, Developer
source-git-commit: 174ed3b35edeb26b09b04bc7d88111a5719e08f8
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# ACSD-58008：終了日をとして編集 *空* スケジュールの更新が表示されなくなります

ACSD-58008 パッチは、終了日をとして編集する問題を修正します *空* スケジュールの更新が表示されなくなります。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされています。 パッチ ID は ACSD-58008 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

終了日をとして編集 *空* スケジュールの更新が表示されなくなります

<u>再現手順</u>:

1. 別のユーザーとしてログイン [!UICONTROL Admin].
1. に移動 **[!UICONTROL Content]** > **[!UICONTROL Elements]** > **[!UICONTROL Pages]** ページを作成します。
1. 作成したページを選択し、「」をクリックします。 **[!UICONTROL Schedule New Update]**. *（ページの右上隅に移動します）*.
1. 4 つの更新を作成します。 *（例：の増分* 2 *分）*.
1. を更新 *更新 2* 時刻を直前の時刻に変更します *更新 4*.
1. 行われた更新を保存します。

<u>期待される結果</u>:

スケジュールの更新には、 *更新 3*.

<u>実際の結果</u>:

スケジュールの更新で「」が表示されない *更新 3*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。