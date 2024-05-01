---
title: 'ACSD-49877：ビデオの自動再生がモバイルで機能しない [!DNL Safari]'
description: ACSD-49877 パッチを適用すると、モバイルでビデオの自動再生オプションが機能しないAdobe Commerceの問題を修正できます [!DNL Safari] ビデオがリモートビデオファイルに直接リンクされている場合。
exl-id: 454f7cec-29b9-485b-93be-2a4f2eb77da7
feature: CMS
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# ACSD-49877：ビデオの自動再生がモバイルで機能しない [!DNL Safari]

ACSD-49877 は、モバイルで自動再生オプションが使用される問題を修正します [!DNL Safari] ビデオがリモートビデオファイルに直接リンクされている場合、は機能しません。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は ACSD-49877 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 [!magento/quality-patches] を最新バージョンにパッケージ化し、[[!DNL Quality Patches Tool]：パッチを検索 ]。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ビデオの自動再生がモバイルで機能しない [!DNL Safari] ビデオがストリーミングサービスではなく、リモートビデオファイルに直接リンクされている場合。

<u>前提条件</u>:
[!DNL Page Builder] モジュールがインストールされている。

<u>再現手順</u>:

1. 新しい CMS ページを作成し、を編集します **[!UICONTROL Content Value]** （を使用） [!DNL Page Builder].
1. を追加 *タブ* 要素をコンテンツに追加して、 *ビデオ要素* 内 *タブ*.
1. 歯車ボタンをクリックして、 *ビデオ要素*.
1. mp4 ビデオファイルへのリンクの追加 [!UICONTROL Video URL] フィールド。
1. マーク **[!UICONTROL Autoplay]** フィールド名 *はい*.
1. クリック **[!UICONTROL Save]**.
1. で最近作成したページを開きます [!DNL Safari] iPhoneを使用する。

<u>期待される結果</u>

自動再生オプションは次の場合に機能します [!DNL Safari] iPhoneを使用する。

<u>実際の結果</u>

自動再生オプションがに対して機能しない [!DNL Safari] iPhoneを使用する。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
