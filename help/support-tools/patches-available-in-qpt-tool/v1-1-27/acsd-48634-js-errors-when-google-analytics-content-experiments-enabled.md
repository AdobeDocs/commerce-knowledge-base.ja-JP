---
title: 'ACSD-48634: [!DNL JS] エラー条件 [!DNL Google Analytics Content Experiments] 有効'
description: 修正する ACSD-48634 パッチを適用します [!DNL JS] エラー状況 [!DNL staging] 更新日時 [!DNL Google Analytics Content Experiments] が有効になっています。
exl-id: 4a9f201d-eaf0-4e43-a1a1-0a9ffb0a2ead
feature: Catalog Management, Categories, Console, Page Content
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# ACSD-48634: [!DNL JS] エラー条件 [!DNL Google Analytics Content Experiments] enabled

ACSD-48634 パッチの修正 [!DNL JS] エラー状況 [!DNL staging] 更新日時 [!DNL Google Analytics Content Experiments] が有効になっています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされています。 パッチ ID は ACSD-48634 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL JS] エラーは次で発生： [!DNL staging] 更新日時 [!DNL Google Analytics Content Experiments] が有効になっています。

<u>再現手順</u>:

1. 対象： **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL All Stores]**、追加の web サイトを作成、格納および **[!UICONTROL Store View]**. 必ずを実行してください **[!UICONTROL Store View]** 等しい *[!UICONTROL Enabled]*.
1. 設定 **[!DNL Configure Google Analytics]** ～に行くことによって **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Google API]**:
   * の場合 **[!DNL Main]** とその他の web サイト [!DNL scope]:
      * **[!UICONTROL Enabled]**: *[!UICONTROL Yes]*
      * **[!UICONTROL Account type]**: *[!UICONTROL Google Tag Manager]*
      * **[!UICONTROL Anonymize IP]**: *[!UICONTROL Yes]*
      * **[!UICONTROL Enable Content Experiments]**: *[!UICONTROL Yes]*
      * **[!UICONTROL Container Id]**: *[!UICONTROL (GTM container ID)]*
      * **[!DNL Uncheck]** *[!UICONTROL Use Default]* その他のフィールドの場合は、変更しないでください。
   * の場合 **[!DNL Default Config]** [!DNL scope]:
      * **[!UICONTROL Enabled]**: *[!UICONTROL Yes]*
      * **[!UICONTROL Account type]**: *[!UICONTROL Universal Analytics]*
      * **[!UICONTROL Account Number]**: *[!UICONTROL (Universal Analytics account number)]*
      * **[!UICONTROL Anonymize IP]**: *[!UICONTROL Yes]*
      * **[!UICONTROL Enable Content Experiments]**: *[!UICONTROL Yes]*
1. 無効 **[!DNL Configure Google Analytics]** 日付： **[!DNL Default Config]** [!DNL scope] 変更による **[!UICONTROL Enable]** から *[!UICONTROL Yes]* 対象： *[!UICONTROL No]*. 他の設定は変更しないでください。
1. に移動 **[!UICONTROL Catalog]** > **[!UICONTROL Categories]**.
1. 作成と編集 **[!UICONTROL category]** スケジュールされた更新を追加します。
   * 任意の名前、将来の開始日、将来の終了日および変更 **[!UICONTROL category]** （[!UICONTROL For Example]: *[!UICONTROL disable category]*）に設定します。
1. 更新を保存して、 [!DNL browser developer console] （エラーの場合）

<u>期待される結果</u>:

不可 [!DNL JS] エラーと変更点 [!DNL staging] 更新は正常に保存されました。

<u>実際の結果</u>:

[!DNL JS] エラーがコンソールに表示され、フォームの形式が正しくない。 [!DNL spinner] 保存後に無効になることはありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
