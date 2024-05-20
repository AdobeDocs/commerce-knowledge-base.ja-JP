---
title: 「ACSD-52219：ブックマーク表示の切り替えでの管理グリッドフィルターの問題の解決」
description: ブックマークビューを頻繁に切り替えると、管理グリッドの保存されたフィルターが期待どおりに動作しないAdobe Commerceの問題を修正するために、ACSD-52219 パッチを適用してください。
feature: Admin Workspace
role: Admin
exl-id: e8333ee7-28a8-4457-aeff-6828f8ca9412
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# ACSD-52219：ブックマーク表示の切り替えでの管理グリッドフィルターの問題の解決

ACSD-52219 パッチは、ブックマークビューを頻繁に切り替えると管理グリッドの保存されたフィルターが期待どおりに動作しない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.39 がインストールされています。 パッチ ID は ACSD-52219 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ブックマーク表示を頻繁に切り替える場合、管理グリッドに保存されたフィルターは、意図したとおりに機能しません。

<u>再現手順</u>:

1. へのアクセス [!DNL Sales Order] 管理画面のグリッド。
1. 2～3 つのフィルターを作成します。
1. ビューを切り替えてフィルター設定を検証し、正確に保存されていることを確認します。
1. Filter1 または Filter2 に移動します。
1. ページを更新して、表示されたデータを更新します。
1. 別のビューに切り替えると、フィルターは変更されません。
1. 特定のフィルターが設定されていない場合でも、デフォルトのビューにフィルター適用済みの結果が表示されていることに注意してください。

<u>期待される結果</u>:

フィルターは入れ替わらず、元の状態を維持します。

<u>実際の結果</u>:

ビューを変更すると、フィルターが混ざり、正しいビューが保存されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
