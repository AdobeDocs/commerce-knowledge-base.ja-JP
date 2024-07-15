---
title: 「ACSD-49877：ビデオの自動再生がモバイルで機能しない  [!DNL Safari]」
description: ビデオがリモートビデオファイルに直接リンクされている場合に、ビデオの自動再生オプションがモバイルで機能しないAdobe Commerceの問題を修正するため  [!DNL Safari] ACSD-49877 パッチを適用してください。
exl-id: 454f7cec-29b9-485b-93be-2a4f2eb77da7
feature: CMS
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# ACSD-49877：ビデオの自動再生がモバイル [!DNL Safari] で機能しない

ACSD-49877 は、ビデオがリモートビデオファイルに直接リンクされている場合に、モバイル [!DNL Safari] の自動再生オプションが機能しない問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされている場合に使用できます。 パッチ ID は ACSD-49877 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、[!magento/quality-patches] パッケージを最新のバージョンに更新し、[[!DNL Quality Patches Tool]：パッチを検索 ] ページで互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ビデオがストリーミングサービスではなくリモートビデオファイルに直接リンクされている場合、ビデオの自動再生がモバイル [!DNL Safari] で機能しません。

<u> 前提条件 </u>:
[!DNL Page Builder] 個のモジュールがインストールされています。

<u> 再現手順 </u>:

1. 新しい CMS ページを作成し、[!DNL Page Builder] で **[!UICONTROL Content Value]** を編集します。
1. *Tab* 要素をコンテンツに追加し、*Tab* 内に *ビデオ要素* を追加します。
1. 次に、歯車ボタンをクリックして *ビデオ要素* を編集します。
1. [!UICONTROL Video URL] フィールドに mp4 ビデオファイルへのリンクを追加します。
1. 「**[!UICONTROL Autoplay]**」フィールドを *はい* としてマークします。
1. 「**[!UICONTROL Save]**」をクリックします。
1. iPhoneを使用して、[!DNL Safari] で最近作成したページを開きます。

<u> 期待される結果 </u>

自動再生オプションは、iPhoneを使用する [!DNL Safari] で機能します。

<u> 実績 </u>

iPhoneを使用している [!DNL Safari] ーザーでは、自動再生オプションは機能しません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
