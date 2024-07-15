---
title: 「ACSD-56858:B2B 会社管理者の役割の権限の不一致」
description: ACSD-56858 パッチを適用すると、B2B 環境で制限された会社管理者のロール権限が正しく表示されないAdobe Commerceの問題を修正できます。
feature: Companies, B2B, Roles/Permissions
role: Admin, Developer
exl-id: d446f815-78bf-42ec-bc2b-a5934b15b416
source-git-commit: 4bf5deb1115705560acc8410441219943329c1a4
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# ACSD-56858:B2B 会社管理者の役割の権限の不一致

ACSD-56858 パッチでは、B2B 環境の制限された会社管理者に対して役割の権限が正しく表示されない問題を修正しています。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.47 がインストールされている場合に使用できます。 パッチ ID は ACSD-56858 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

B2B 環境で制限された会社管理者の役割の権限が正しく表示されません。

<u> 再現手順 </u>:

1. 会社の設定から開始し、会社管理者と会社ユーザーを追加します。
1. ストアフロントで会社管理者としてログインし、様々なユーザー向けの様々な役割を作成します。
1. 必要に応じてこれらの役割を割り当てます。例えば、一部のタスクにはアクセスを制限し、他のタスクには完全なアクセスを許可します。
1. これらの役割を、会社管理者以外のユーザーへのフルアクセス権で割り当てます。
1. 会社以外の管理者ユーザー（会社_manager など）にログインします。
1. **[!UICONTROL Roles and permission]** に移動し、役割を編集します。
1. 表示される権限は、その役割 ID に対して会社のデータベースに設定された権限と一致しないことに注意してください。

<u> 期待される結果 </u>:

会社以外の管理者ユーザーの役割と権限は正しく表示されます。

<u> 実際の結果 </u>:

権限テーブルのデータベースレコードに従って、会社以外の管理者ユーザーの役割が正しく表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
