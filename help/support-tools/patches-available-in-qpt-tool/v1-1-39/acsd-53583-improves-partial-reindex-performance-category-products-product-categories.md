---
title: 'ACSD-53583：部分的な再インデックスパフォーマンスの向上 [!UICONTROL Category Products] および [!UICONTROL Product Categories] インデクサー'
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

ACSD-53583 パッチにより、の部分的な再インデックスのパフォーマンスが向上します。 *カテゴリ製品* および *製品カテゴリ* インデクサー。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.39 がインストールされています。 パッチ ID は ACSD-53583 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3
* と互換性がありません [!DNL Live Search] モジュール。 このパッチを適用するには [!DNL Live Search] インストールするには、追加の ACSD-55719 パッチを要求してください。

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

部分的な再インデックス化は、完全な再インデックス化よりも時間がかかります。

<u>再現手順</u>:

1. すべてのインデクサーを次の値に変更： *スケジュールで更新*.
1. でのデータの生成 [!DNL Performance Toolkit] （中背）。
1. すべての製品とカテゴリを変更して、インデックスがバックログに残り、すべてのインデックスがアイドル状態になるようにします。
1. に対して部分再インデックスを実行 *カテゴリ製品* および *製品カテゴリ* インデクサー。

<u>期待される結果</u>:

部分的な再インデックスは、製品ごとに 1 回呼び出されます。すべての製品とカテゴリが変更されているので、完全な再インデックスとほぼ同じ時間がかかります。

<u>実際の結果</u>:

部分再インデックスは、製品ごとに何度も呼び出され、完全な再インデックスよりも時間がかかります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
