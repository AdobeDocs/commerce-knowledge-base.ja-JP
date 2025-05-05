---
title: 「ACSD-51528:snake_case 形式の異なる動作」
description: ACSD-51528 パッチを適用して、snake_case 形式で異なる動作が発生するAdobe Commerceの問題を修正してください。
exl-id: dd878321-8032-41f3-8dcd-acb0cc023b44
feature: Variables
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# ACSD-51528: snake_case 形式の異なる動作

ACSD-51528 パッチは、snake_case 形式の様々な動作を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされている場合に使用できます。 パッチ ID は ACSD-51528 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

snake_case フォーマット設定の異なる動作。

<u> 再現手順 </u>:

1. 様々なプロパティ名を使用して `\Magento\Framework\Api\DataObjectHelper::populateWithArray` 関数をテストします。
1. *NewPName* のような名前を持つプロパティは、*new_p_name* に変換する必要があります。代わりに、*new_pname* に変換されます。
1. また、オブジェクトで *getNewPName* 関数を使用すると、*Abstract モデル* が *new_p_name* への呼び出しを正しく変換し、両方の関数が互いに互換性を持たなくなるので、*null* が返されます。

<u> 期待される結果 </u>

**[!UICONTROL populateWithArray]** 関数は、オブジェクトのプロパティを snake_case に正しく変換し、**[!DNL AbstractModel's]** `Getters` および `Setters` と互換性を持たせる必要があります。

<u> 実績 </u>

**[!UICONTROL populateWithArray]** 関数を使用する場合、名前に 2 つ以上の大文字が行に含まれているオブジェクトプロパティにより、最終的なデータ配列で snake_case 変換が正しく行われなくなります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
