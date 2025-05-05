---
title: 「ACSD-52219：ブックマーク表示の切り替えでの管理グリッドフィルターの問題の解決」
description: ブックマークビューを頻繁に切り替えると、管理グリッドの保存されたフィルターが期待どおりに動作しないAdobe Commerceの問題を修正するために、ACSD-52219 パッチを適用してください。
feature: Admin Workspace
role: Admin
exl-id: e8333ee7-28a8-4457-aeff-6828f8ca9412
source-git-commit: dccb8dde1666fa0c72c7c94cd94c82daddaadc54
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# ACSD-52219：ブックマーク表示の切り替えでの管理グリッドフィルターの問題の解決

ACSD-52219 パッチは、ブックマークビューを頻繁に切り替えると管理グリッドの保存されたフィルターが期待どおりに動作しない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.39 がインストールされている場合に使用できます。 パッチ ID は ACSD-52219 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ブックマーク表示を頻繁に切り替える場合、管理グリッドに保存されたフィルターは、意図したとおりに機能しません。

<u> 再現手順 </u>:

1. 管理者の [!DNL Sales Order] グリッドにアクセスします。
1. 2～3 つのフィルターを作成します。
1. ビューを切り替えてフィルター設定を検証し、正確に保存されていることを確認します。
1. Filter1 または Filter2 に移動します。
1. ページを更新して、表示されたデータを更新します。
1. 別のビューに切り替えると、フィルターは変更されません。
1. 特定のフィルターが設定されていない場合でも、デフォルトのビューにフィルター適用済みの結果が表示されていることに注意してください。

<u> 期待される結果 </u>:

フィルターは入れ替わらず、元の状態を維持します。

<u> 実際の結果 </u>:

ビューを変更すると、フィルターが混ざり、正しいビューが保存されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
