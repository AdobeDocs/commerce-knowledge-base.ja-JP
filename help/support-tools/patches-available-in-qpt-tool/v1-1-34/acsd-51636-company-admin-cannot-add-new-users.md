---
title: 「ACSD-51636：会社管理者が顧客アカウントセクションから新しいユーザーを追加できない」
description: ACSD-51636 パッチを適用すると、必要な役割と権限がすべて揃っているにもかかわらず、会社管理者がカスタマーアカウント セクションから新しいユーザーを追加できないAdobe Commerceの問題を修正できます。
feature: Admin Workspace, B2B, Companies, Customer Service
role: Admin
exl-id: 78395584-e5d3-414e-859d-a68ce1af5af1
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# ACSD-51636：会社管理者が顧客アカウントセクションから新しいユーザーを追加できない

ACSD-51636 パッチは、必要な役割と権限がすべて揃っているにもかかわらず、会社の管理者が顧客アカウント セクションから新しいユーザーを追加できない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.34 がインストールされています。 パッチ ID は ACSD-51636 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

会社管理者は、必要な役割と権限がすべて揃っているにもかかわらず、顧客アカウントセクションから新しいユーザーを追加できません。

前提条件：

* B2B モジュールがインストールされています。
* 会社機能が有効になっています。

<u>再現手順</u>:

1. 新しい会社を作成します。
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Customers]** > **[!UICONTROL All Customers]**.
1. 編集 **[!UICONTROL Company Admin]** type to *顧客*.
1. 顧客としてログインします。
1. に移動 **[!UICONTROL My Account]** > **[!UICONTROL Company Users]** > **[!UICONTROL Add User]** さらに、ユーザーの詳細を追加し、アクティブにします。
1. 新規ユーザーを保存します。

<u>期待される結果</u>

管理者ユーザーは、新しいユーザーを追加できます。

<u>実際の結果</u>

* 管理者ユーザーに次のエラーメッセージが表示されます。 *エラーが発生しました*.
* 管理者ユーザーは、新しい顧客を作成できません。
* ログには、次のエラーが含まれます。

  ```PHP
      report.CRITICAL: Error: Call to a member function __toArray() on null in app/code/Magento/LoginAsCustomerLogging/Observer/LogSaveCustomerObserver.php:123
  ```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
