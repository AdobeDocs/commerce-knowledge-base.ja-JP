---
title: 「ACSD-51149：有効な [!UICONTROL Catalog Permissions] でインデクサーを無効にするスケジュールされた [!UICONTROL ImportExport]」
description: ACSD-51149 パッチを適用して、[!UICONTROL Catalog Permissions] が有効になっているスケジュール済み [!UICONTROL ImportExport] がインデクサーを無効にするAdobe Commerceのパフォーマンスの問題を修正してください。
feature: Cache, Data Import/Export
role: Admin
exl-id: 3a26f4be-8e52-407d-bb25-2841458f3aa5
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# ACSD-51149：有効な [!UICONTROL Catalog Permissions] を持つスケジュールされた [!UICONTROL ImportExport] ールでインデクサーを無効にします

ACSD-51149 パッチは、が有効になっているスケジュールされた [!UICONTROL ImportExport] がインデクサーを無効にする問題を修正 [!UICONTROL Catalog Permissions] ます。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされている場合に使用できます。 パッチ ID は ACSD-51149 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 - 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!UICONTROL Catalog Permissions] が有効なスケジュールされた [!UICONTROL ImportExport] はインデクサーを無効にします。

<u> 再現手順 </u>:

1. *[!UICONTROL Catalog Permissions]* を有効にします。
1. すべてのインデクサーを *[!UICONTROL Update by Schedule]* に設定します。
1. シンプルな製品を作成します。
1. **[!UICONTROL System]**/**[!UICONTROL Data Transfer]**/**[!UICONTROL Export]** を使用して、この製品を書き出します。
1. 書き出した CSV をダウンロードし、`<AC root folder>/var/import` に入れます。
1. ダウンロードした CSV を使用して、スケジュールされた製品読み込みを作成します。
1. 完全な再インデックスを実行します。
1. インデクサーのステータスを確認します。 すべてのインデクサーは *[!UICONTROL Ready]* ステータスである必要があります。
1. 作成したスケジュール済み読み込みをグリッドから実行します。
1. インデクサーのステータスを再確認します。

<u> 期待される結果 </u>:

すべてのインデクサーは *[!UICONTROL Ready]* ステータスです。

<u> 実際の結果 </u>:

一部のインデクサーは *[!UICONTROL Reindex Required]* 状態です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
