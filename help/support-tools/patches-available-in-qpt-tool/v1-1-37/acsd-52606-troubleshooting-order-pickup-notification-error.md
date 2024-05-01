---
title: 「ACSD-52606：ユーザーが「注文の受け取りの準備が整ったことを通知」をクリックすると表示されるエラーメッセージ」
description: ACSD-52606 パッチを適用すると、ユーザーが**をクリックしたときにエラーメッセージが表示されるAdobe Commerceの問題を修正できます[!UICONTROL Notify Order is Ready for Pickup]**。
feature: Orders, User Account
role: Admin, Developer
exl-id: c3e69eb1-90bf-46cf-9b53-110e40e0c3c1
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# ACSD-52606：ユーザーが「注文の受け取りの準備が整ったことを通知」をクリックすると表示されるエラーメッセージ

ACSD-52606 パッチは、エラーメッセージが表示される問題を修正します *注文を受け取る準備ができていません* ユーザーがクリックしたときに表示されます。 **[!UICONTROL Notify Order is Ready for Pickup]**. このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.37 がインストールされています。 パッチ ID は ACSD-52606 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

エラーメッセージ *注文を受け取る準備ができていません* は、ユーザーがクリックすると画面に表示されます **[!UICONTROL Notify Order is Ready for Pickup]**.

<u>前提条件</u>:

インベントリモジュールがインストールされます。

<u>再現手順</u>:

1. 新しいインスタンスをインストールします。
1. 新しいソースと在庫を作成します。
1. 新しいソースをデフォルトの web サイトに割り当てます。
1. 新しく作成されたソースの取得場所を有効にします。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Delivery Methods]** > **[!UICONTROL In-Store Delivery]** および有効化 **[!UICONTROL In-Store Delivery]**.
1. を作成 *在庫あり* ～を使った簡単な製品 *QTY=0* すべての在庫および *[!UICONTROL Manage Stock = No]* 両方のソースに割り当てます。
1. を選択し、前の手順で作成した製品を使用して、フロントエンドから注文を作成します。 *[!UICONTROL In-Store Pickup]* 配信方法として。
1. 管理者で、に移動します。 **[!UICONTROL Sales]** > **[!UICONTROL Orders]** > **[!UICONTROL Invoice that order]**.
1. クリック **[!UICONTROL Notify order is ready for pickup]**.

<u>期待される結果</u>:

エラーなしで通知されます。

<u>実際の結果</u>:

次のエラーメッセージが表示されます。 *注文を受け取る準備ができていません*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
