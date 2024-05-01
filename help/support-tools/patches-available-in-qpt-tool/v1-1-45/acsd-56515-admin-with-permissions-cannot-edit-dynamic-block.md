---
title: 'ACSD-56515:Web サイトレベルの権限を持つ管理者は、編集できません [!UICONTROL Dynamic Block]'
description: Adobe Commerce ACSD-56515 パッチを適用すると、web サイトレベルの権限を持つ管理者が、 [!UICONTROL Dynamic Block].
feature: Roles/Permissions, Admin Workspace
role: Admin, Developer
exl-id: 5aa6b11e-b467-4076-ad36-162966cbf6df
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# ACSD-56515:Web サイトレベルの権限を持つ管理者は、編集できない [!UICONTROL Dynamic Block]

ACSD-56515 パッチは、web サイトレベルの権限を持つ管理者がを追加または編集できない問題を修正します [!UICONTROL Dynamic Block]. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされています。 パッチ ID は ACSD-56515 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Web サイトレベルの権限を持つ管理者は、を追加または編集できません [!UICONTROL Dynamic Block].

<u>再現手順</u>:

1. store と storereview を使用してセカンダリ web サイトを作成します。
1. に移動 **[!UICONTROL System]** > **[!UICONTROL Permissions]** > **[!UICONTROL User Roles]** さらに、使用可能なすべてのリソースを使用して、セカンダリ web サイト範囲に制限されたユーザーの役割を作成します。
1. 管理者ユーザーを、上記で作成した役割で作成します。
1. 制限付きの管理者ユーザーでログインし、 [!UICONTROL Dynamic Block].

<u>期待される結果</u>:

Web サイトに対する制限を持つ管理者ユーザーは、 [!UICONTROL Dynamic Block].

<u>実際の結果</u>:

次のエラーが発生します。 *この項目を表示するには、さらに権限が必要です*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
