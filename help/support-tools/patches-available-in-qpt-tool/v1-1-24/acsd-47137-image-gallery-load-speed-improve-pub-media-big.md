---
title: '''ACSD-47137：画像ギャラリーの読み込み速度の向上''pub/media'' フォルダーが大きい'''
description: 「pub/media」フォルダーが非常に大きい場合は、画像ギャラリーの読み込み速度を向上させるために ACSD-47137 パッチを適用します。
exl-id: 43268909-6845-4d1d-b6b8-4ae0ce40fd5e
feature: Cache, Catalog Management, Categories, Media
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# ACSD-47137：画像ギャラリーの読み込み速度を向上 `pub/media` フォルダーが大きい

ACSD-47137 パッチは、次の場合に画像ギャラリーの読み込み速度を向上させます `pub/media` フォルダーはとても大きい。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされています。 パッチ ID は ACSD-47137 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

次の場合、画像ギャラリーの読み込み速度が遅くなります。 `pub/media` フォルダーはとても大きい。

<u>再現手順</u>:

1. Adobe Commerce管理者に移動します **[!UICONTROL STORES]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Media Gallery]** > **[!UICONTROL Enable Old Media Gallery]** 対象： _不可_.
1. 設定キャッシュをクリーンアップします。
1. ログアウトして、管理者ユーザーとして再度ログインします。
1. 管理サイドバーで、に移動します。 **[!UICONTROL Catalog]** > **[!UICONTROL Categories]** ルートカテゴリを選択します。
1. を展開します。 **[!UICONTROL Content]** セクションのをクリックし、 **[!UICONTROL Select from Gallery]**.

ページを読み込むと、Adobe Commerceは次を送信します `media_gallery/directories/gettree` メディア フォルダ ツリーの読み込み要求。

<u>期待される結果</u>:

この `media_gallery/directories/gettree` リクエストでは、パスリスト全体をからループさせる以外に、必要なディレクトリからのみコンテンツを読み込む必要があります。 `pub/media/` フォルダー。

<u>実際の結果</u>:

この `media_gallery/directories/gettree` 次の場合、リクエストの読み込みに時間がかかる： `pub/media/` フォルダーには多くのコンテンツがあります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
