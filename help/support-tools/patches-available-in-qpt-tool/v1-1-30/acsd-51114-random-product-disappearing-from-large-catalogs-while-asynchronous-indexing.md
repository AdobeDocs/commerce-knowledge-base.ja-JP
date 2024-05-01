---
title: 「ACSD-51114：非同期インデックス作成が有効になっている場合、大規模なカタログからランダムな製品が表示されなくなる」
description: ACSD-51114 パッチを適用して、Adobe Commerceの問題を修正してください。非同期インデックス作成が有効な場合、大きなカタログからランダムな製品が消えました。
exl-id: 6ea7de32-1d30-4c4a-af6e-6a0931396846
feature: Catalog Management, Categories, Products
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# ACSD-51114：非同期インデックス作成が有効になっている場合、大規模なカタログからランダムな製品が消えた

>[!NOTE]
>
>このパッチは非推奨（廃止予定）です。

ACSD-51114 パッチは、非同期インデックス作成が有効な場合に、大きなカタログからランダムな製品が表示されなくなる問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は ACSD-51114 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、[[!DNL Quality Patches Tool]：パッチを検索するページ ]。パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

非同期インデックス作成が有効になっている場合、大規模なカタログからランダムな製品が消えました。

<u>再現手順</u>:

1. 10 個の商品セットを作成します。
1. すべてのインデクサーをに設定 **[!UICONTROL Update on Save]** モード。
1. カテゴリを作成し、すべての製品を割り当てます。
1. すべての製品を無効にします。
1. カテゴリを開き、製品がないことを確認します。
1. すべてのインデクサーをに設定 **[!UICONTROL Update on Schedule]** モード。
1. を `DEFAULT_BATCH_SIZE` 2 インチまで  `lib/internal/Magento/Framework/Mview/View.php#L31`.
1. 1 番目、9 番目、2 番目、5 番目、10 番目、3 番目の順序で製品を有効にします。
1. cron コマンドを実行します。
1. カテゴリを再度開きます。

<u>期待される結果</u>:

有効な製品がすべて表示されます。

<u>実際の結果</u>:

有効な製品はすべて表示されるわけではありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
