---
title: 'ACSD-51149: スケジュール型 [!UICONTROL ImportExport] が有効の場合 [!UICONTROL Catalog Permissions] インデクサーを無効にします'
description: がスケジュールされているAdobe Commerceのパフォーマンスの問題を修正するには、ACSD-51149 パッチを適用します [!UICONTROL ImportExport] が有効の場合 [!UICONTROL Catalog Permissions] インデクサーを無効にします。
feature: Cache, Data Import/Export
role: Admin
exl-id: 3a26f4be-8e52-407d-bb25-2841458f3aa5
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# ACSD-51149: スケジュール型 [!UICONTROL ImportExport] が有効の場合 [!UICONTROL Catalog Permissions] インデクサーを無効にします

ACSD-51149 パッチは、がスケジュールされた問題を修正します [!UICONTROL ImportExport] が有効の場合 [!UICONTROL Catalog Permissions] インデクサーを無効にします。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-51149 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

スケジュール済み [!UICONTROL ImportExport] が有効の場合 [!UICONTROL Catalog Permissions] インデクサーを無効にします。

<u>再現手順</u>:

1. Enable （有効） *[!UICONTROL Catalog Permissions]*.
1. すべてのインデクサーをに設定 *[!UICONTROL Update by Schedule]*.
1. シンプルな製品を作成します。
1. この製品のエクスポート方法 **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Export]**.
1. 書き出した CSV をダウンロードし、に配置します。 `<AC root folder>/var/import`.
1. ダウンロードした CSV を使用して、スケジュールされた製品読み込みを作成します。
1. 完全な再インデックスを実行します。
1. インデクサーのステータスを確認します。 すべてのインデクサーはにあります *[!UICONTROL Ready]* ステータス。
1. 作成したスケジュール済み読み込みをグリッドから実行します。
1. インデクサーのステータスを再確認します。

<u>期待される結果</u>:

すべてのインデクサーは *[!UICONTROL Ready]* ステータス。

<u>実際の結果</u>:

一部のインデクサーは *[!UICONTROL Reindex Required]* ステータス。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
