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

ACSD-53722 パッチは、異なるスコープのスケジュールされたアップデートがアクティブになると、バンドルされた製品オプションの価格が$0 に変更される問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.41 がインストールされている場合に使用できます。 パッチ ID は ACSD-53722 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

異なる範囲のスケジュールされたアップデートがアクティブになると、バンドルされた製品オプションの価格は$0 に変更されます。

<u> 再現手順 </u>:

1. A と B の 2 つの web サイトを作成します。
1. **[!UICONTROL Catalog]** > **[!UICONTROL Price]** > **[!UICONTROL Catalog Price Scope]** = **[!UICONTROL Website]** で設定を指定します。
1. Web サイト A および B で、固定価格のバンドル製品を作成します。

   * バンドル製品価格=固定= *0*

1. バンドルのドロップダウンオプションとして 1 つのシンプルな製品を追加します。 次の価格を設定します。

   * シンプルな製品のすべての店舗ビュー価格はバンドルされたオプション = *120*
   * シンプルな製品のウェブサイト バンドルオプション内の価格= *130*
   * 単純な製品の Web サイト B の価格はバンドルされたオプション = *140*

1. Web サイト A でバンドルされた製品を無効にするアップデートをスケジュールします。

<u> 期待される結果 </u>:

Web サイト A の更新予定は、Web サイト B の価格には影響しません。

<u> 実際の結果 </u>:

スケジュールされた更新後、web サイト B のバンドルされた製品オプションの価格は **$0** に変更されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
