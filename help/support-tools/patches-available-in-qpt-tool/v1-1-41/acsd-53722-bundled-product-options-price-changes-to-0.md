---
title: 「ACSD-53722：バンドルされた製品オプションの価格が 0 ドルに変更」
description: ACSD-53722 パッチを適用すると、異なる範囲のスケジュールされたアップデートがアクティブになると、バンドルされた製品オプションの価格が$0 に変わるAdobe Commerceの問題を修正できます。
feature: Products
role: Admin, Developer
exl-id: da4c25ac-78bc-4d4e-a55e-826924a099e9
source-git-commit: e587b70a270bca624fb60a1b0940c05221da3aef
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# ACSD-53722: バンドルされた製品オプションの価格が$0 に変更されました

ACSD-53722 パッチは、異なるスコープのスケジュールされたアップデートがアクティブになると、バンドルされた製品オプションの価格が$0 に変更される問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.41 がインストールされています。 パッチ ID は ACSD-53722 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

異なる範囲のスケジュールされたアップデートがアクティブになると、バンドルされた製品オプションの価格は$0 に変更されます。

<u>再現手順</u>:

1. A と B の 2 つの web サイトを作成します。
1. 次の下で設定 **[!UICONTROL Catalog]** > **[!UICONTROL Price]** > **[!UICONTROL Catalog Price Scope]** = **[!UICONTROL Website]**.
1. Web サイト A および B で、固定価格のバンドル製品を作成します。

   * バンドル製品価格=固定= *0*

1. バンドルのドロップダウンオプションとして 1 つのシンプルな製品を追加します。 次の価格を設定します。

   * シンプルな製品のすべての店舗ビュー価格はバンドルされているオプション = *120*
   * シンプルな製品の Web サイト バンドルオプション内の価格= *130*
   * 単純な製品の Web サイト B の価格はバンドルされたオプション = *140*

1. Web サイト A でバンドルされた製品を無効にするアップデートをスケジュールします。

<u>期待される結果</u>:

Web サイト A の更新予定は、Web サイト B の価格には影響しません。

<u>実際の結果</u>:

スケジュールされた更新後、web サイト B のバンドルされた製品オプションの価格が「」に変更されます **$0**.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
