---
title: '''ACSD-47336: [!UICONTROL Something went wrong] Adobe Commerce管理者の通知でエラーが発生する'
description: ACSD-47336 パッチを適用して、ユーザーに表示されるAdobe Commerceの問題を修正します [!UICONTROL Something went wrong] で通知を却下する際にエラーが発生する [!DNL Commerce] 管理者。
exl-id: 7561f055-ce04-4a49-8c58-271c24420a60
feature: Admin Workspace
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# ACSD-47336: _[!UICONTROL Something went wrong]_Adobe Commerce Admin で通知を却下する際にエラーが発生する

ACSD-47336 パッチは、ユーザーに表示される問題を修正します。 _[!UICONTROL Something went wrong]_で通知を却下する際にエラーが発生する [!DNL Commerce] 管理者。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされています。 パッチ ID は ACSD-47336 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法）:2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法）:2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーに対する表示 _[!UICONTROL Something went wrong]_で通知を却下する際にエラーが発生する [!DNL Commerce] 管理者。

<u>再現手順</u>:

1. 一括操作（製品グリッドからの製品属性の一括更新など）を実行します。
1. 操作を完了する（例： `bin/magento queue:consumer:start product_action_attribute.update`）に設定します。
1. を更新 [!DNL Commerce] 「管理者」ページで「管理者通知」セクションを展開し、 **[!UICONTROL Dismiss All Completed Tasks]** リンク。

<u>期待される結果</u>:

この _[!UICONTROL Something went wrong]_完了したタスクをクリアする際に、エラーが表示されないようにする。

<u>実際の結果</u>:

この _[!UICONTROL Something went wrong]_エラーが表示される。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
