---
title: 「ACSD-48694：無効な状態変更リクエストのエラーにより、お客様が注文できない」
description: ACSD-48694 パッチを適用すると、「Invalid state change requested （無効なステート変更がリクエストされました）」というエラーによって、お客様の注文が妨げられるAdobe Commerceの問題が修正されます。
exl-id: edf79424-6c4f-4cfd-ab7e-19f95b9bc685
feature: Admin Workspace, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# ACSD-48694: *無効な状態変更が要求されました* エラーにより、お客様が注文できない

ACSD-48694 パッチは、エラーが発生する問題を修正します *無効な状態変更が要求されました* 顧客が注文できないようにします。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされています。 パッチ ID は ACSD-48694 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.37-p4、2.4.1 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

エラー *無効な状態変更が要求されました* 顧客が注文できないようにします。

<u>再現手順</u>:

1. の間にわずかな遅延を追加 `/estimate-shipping-methods` を含めることによるリクエスト `sleep()` 時刻 `app/code/Magento/Quote/Model/GuestCart/GuestShippingMethodManagement.php::estimateByExtendedAddress()` 関数なので、 `/estimate-shipping-methods` リクエストは、次の期間の後に完了します： `/shipping-information` チェックアウト中に配送手順から支払い手順に進む場合。
1. 使用するセッションの設定 [!DNL Redis] （を使用） *disable_locking: 1* の設定値。
1. 開く **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Customers]** および有効化 *[!UICONTROL Persistent Shopping Cart]*.
1. 顧客としてログインし、商品を買い物かごに追加します。
1. カスタマーセッションの有効期限が切れるようにします。 永続的な Cookie と買い物かごは引き続き保存されます。
1. チェックアウトに移動し、配送先住所を追加して、支払いセクションに移動します。
1. ホームページまたはその他のページに戻り、カスタマーアカウントでログインします。
1. セッションの有効期限をもう一度切ります。
1. 次に、チェックアウトページに直接移動し、支払い手順に移動します。
1. 注文してみてください。

<u>期待される結果</u>:

* エラーはありません。
* 注文が正常に行われ、 *ありがとうございました* ページが表示されます。

<u>実際の結果</u>:

エラー *無効な状態変更が要求されました* が表示されますが、注文が行われます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
