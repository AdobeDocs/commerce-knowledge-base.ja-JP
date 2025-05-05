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

ACSD-51636 パッチは、必要な役割と権限がすべて揃っているにもかかわらず、会社の管理者が顧客アカウント セクションから新しいユーザーを追加できない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.34 がインストールされている場合に使用できます。 パッチ ID は ACSD-51636 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

会社管理者は、必要な役割と権限がすべて揃っているにもかかわらず、顧客アカウントセクションから新しいユーザーを追加できません。

前提条件：

* B2B モジュールがインストールされています。
* 会社機能が有効になっています。

<u> 再現手順 </u>:

1. 新しい会社を作成します。
1. **[!UICONTROL Admin]**/**[!UICONTROL Customers]**/**[!UICONTROL All Customers]** に移動します。
1. **[!UICONTROL Company Admin]** タイプを *顧客* に編集します。
1. 顧客としてログインします。
1. **[!UICONTROL My Account]**/**[!UICONTROL Company Users]**/**[!UICONTROL Add User]** に移動して、ユーザーの詳細を追加し、アクティブにします。
1. 新規ユーザーを保存します。

<u> 期待される結果 </u>

管理者ユーザーは、新しいユーザーを追加できます。

<u> 実績 </u>

* 管理者ユーザーに「*問題が発生しました*」というエラーメッセージが表示される。
* 管理者ユーザーは、新しい顧客を作成できません。
* ログには、次のエラーが含まれます。

  ```PHP
      report.CRITICAL: Error: Call to a member function __toArray() on null in app/code/Magento/LoginAsCustomerLogging/Observer/LogSaveCustomerObserver.php:123
  ```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja>) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja>)」を参照してください。
