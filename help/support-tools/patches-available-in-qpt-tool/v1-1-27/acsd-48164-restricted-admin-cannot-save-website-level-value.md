---
title: 「ACSD-48164：制限付き管理者は、web サイトレベルの値を保存できない」
description: ACSD-48164 パッチを適用して、制限付き管理者が web サイトレベルの値を保存できないAdobe Commerceの問題を修正してください。
exl-id: 6ec15163-ad30-4566-a46c-5756bfd9f8d4
feature: Admin Workspace
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# ACSD-48164：制限付き管理者は、web サイトレベルの値を保存できません

ACSD-48164 パッチは、制限付き管理者が web サイトレベルの値を保存できない問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされています。 パッチ ID は ACSD-48164 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

制限付き管理者は、web サイトレベルの値を保存できません。

<u>再現手順</u>:

1. に新しい web サイト、ストア、ストア表示を作成する [!UICONTROL Admin] > **[!UICONTROL Store]** > **[!UICONTROL All Stores]**.
1. に新しい管理者ロールを作成します。 [!UICONTROL Admin] > **[!UICONTROL System]** > **[!UICONTROL User Roles]**.

   * に移動 **[!UICONTROL Role Resources]** > **[!UICONTROL Role Scopes]**&#x200B;を選択して、新しい web サイトを選択し、この役割を任意の管理者ユーザーに割り当てます。

1. 任意の製品を選択し、新しい web サイトのみを割り当てます。 デフォルトの web サイトは選択しないでください。
1. 手順 2 で割り当てられた管理者ユーザーとしてログインし、の製品を編集します **[!UICONTROL All Store View]** のような web サイトレベルの属性を変更することでスコープを設定する *[!UICONTROL Status]*, *[!UICONTROL Tax Class]*&#x200B;を選択し、製品を新規として設定します。
1. 商品を保存します。

<u>期待される結果</u>:

ある web サイトへの役割スコープに関連付けられている管理者ユーザーは、を使用して web サイトレベルの製品属性を保存できます *[!UICONTROL All Store View]* スコープ。

<u>実際の結果</u>:

製品が保存されたという成功メッセージが表示されますが、製品属性値は変更されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
