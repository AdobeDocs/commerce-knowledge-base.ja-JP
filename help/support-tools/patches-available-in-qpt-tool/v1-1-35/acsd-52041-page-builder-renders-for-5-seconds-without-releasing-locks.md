---
title: 「ACSD-52041：ページビルダーのレンダリングでロックが解放されない」
description: ACSD-52041 パッチを適用して、ページビルダーがロックを解除せずに 5 秒間レンダリングされるAdobe Commerceの問題を修正してください。
feature: Page Builder
role: Admin, Developer
exl-id: f2a1fd36-2098-46a7-aa42-3a5a0014adc9
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# ACSD-52041：ページビルダーのレンダリングでロックが解放されない

ACSD-52041 パッチでは、ロックを解除せずにページビルダーが 5 秒間レンダリングされる問題が修正されています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-52041 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ページビルダーは、ロックを解除せずに 5 秒間レンダリングされます。

<u>再現手順</u>:

1. CMS ページ、製品ページまたはページビルダーを持つものを編集します。
1. 変更を保存します。
1. ページの保存時間に注意してください。

<u>期待される結果</u>

コンテンツが保存されます。 ブラウザーログにエラーは見つかりませんでした。

<u>実際の結果</u>

保存が完了するまでに通常より時間がかかります。
コンソールのエラー： ``Page Builder was rendering for 5 seconds without releasing locks``

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
