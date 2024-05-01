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

ACSD-56858 パッチでは、B2B 環境の制限された会社管理者に対して役割の権限が正しく表示されない問題を修正しています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.47 がインストールされています。 パッチ ID は ACSD-56858 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

B2B 環境で制限された会社管理者の役割の権限が正しく表示されません。

<u>再現手順</u>:

1. 会社の設定から開始し、会社管理者と会社ユーザーを追加します。
1. ストアフロントで会社管理者としてログインし、様々なユーザー向けの様々な役割を作成します。
1. 必要に応じてこれらの役割を割り当てます。例えば、一部のタスクにはアクセスを制限し、他のタスクには完全なアクセスを許可します。
1. これらの役割を、会社管理者以外のユーザーへのフルアクセス権で割り当てます。
1. 会社以外の管理者ユーザー（会社_manager など）にログインします。
1. に移動します。 **[!UICONTROL Roles and permission]** 役割を編集します。
1. 表示される権限は、その役割 ID に対して会社のデータベースに設定された権限と一致しないことに注意してください。

<u>期待される結果</u>:

会社以外の管理者ユーザーの役割と権限は正しく表示されます。

<u>実際の結果</u>:

権限テーブルのデータベースレコードに従って、会社以外の管理者ユーザーの役割が正しく表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
