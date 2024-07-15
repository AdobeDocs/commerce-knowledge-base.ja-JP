---
title: 「ACSD-53583:[!UICONTROL Category Products] および [!UICONTROL Product Categories] インデクサーの部分再インデックスパフォーマンスの向上」
description: ACSD-53585 パッチを適用して、カテゴリ製品および製品カテゴリインデクサーの部分的なインデックス再作成のパフォーマンスを向上させます。
feature: Products, Categories
role: Admin, Developer
exl-id: 1c8f7df3-379f-42d6-8b41-286d34f725d2
source-git-commit: 29c2918ccae6404f6ae87d360ac16b149de5dd0d
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# ACSD-53583：カテゴリ製品および製品カテゴリインデクサーの部分的な再インデックスパフォーマンスの向上

ACSD-53583 パッチにより、*Category Products* および *Product Categories* インデクサーの部分的な再インデックスパフォーマンスが向上します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.39 がインストールされている場合に使用できます。 パッチ ID は ACSD-53583 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3
* [!DNL Live Search] モジュールと互換性がありません。 このパッチをインストールに適用する [!DNL Live Search] は、追加の ACSD-55719 パッチをリクエストしてください。

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

部分的な再インデックス化は、完全な再インデックス化よりも時間がかかります。

<u> 再現手順 </u>:

1. すべてのインデクサーを *スケジュールで更新* に切り替えます。
1. [!DNL Performance Toolkit] （中程度のプロファイル）でデータを生成します。
1. すべての製品とカテゴリを変更して、インデックスがバックログに残り、すべてのインデックスがアイドル状態になるようにします。
1. *カテゴリ製品* および *製品カテゴリ* インデクサーに対して部分再インデックスを実行します。

<u> 期待される結果 </u>:

部分的な再インデックスは、製品ごとに 1 回呼び出されます。すべての製品とカテゴリが変更されているので、完全な再インデックスとほぼ同じ時間がかかります。

<u> 実際の結果 </u>:

部分再インデックスは、製品ごとに何度も呼び出され、完全な再インデックスよりも時間がかかります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
