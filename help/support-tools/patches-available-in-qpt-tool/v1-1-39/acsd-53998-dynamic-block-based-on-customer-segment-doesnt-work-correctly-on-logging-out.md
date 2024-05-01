---
title: 「ACSD-53998：顧客セグメントに基づく動的ブロックがログアウト後に正しく機能しない」
description: ACSD-53998 パッチを適用すると、カスタマーアカウントからログアウトした後、カスタマーセグメントに基づく動的ブロックが正しく機能しないAdobe Commerceの問題を修正できます。
feature: Customers, Page Builder, Personalization
role: Admin, Developer
exl-id: 5a82a6b8-e8f7-47ff-89f6-93a39b72fe38
source-git-commit: dccb8dde1666fa0c72c7c94cd94c82daddaadc54
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# ACSD-53998：顧客セグメントに基づく動的ブロックがログアウト後に正しく機能しない

ACSD-53998 パッチは、顧客アカウントからログアウトした後、顧客セグメントに基づく動的ブロックが正しく機能しない問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.39 がインストールされています。 パッチ ID は ACSD-53998 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2 - 2.4.4-p6、2.4.5-p1 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

顧客セグメントに基づく動的ブロックは、顧客アカウントからログアウトした後、正しく機能しません。

<u>前提条件</u>:

のインストールと有効化 [!DNL Page Builder] モジュール。

<u>再現手順</u>:

1. 条件なしで 2 つの顧客セグメントを作成します。
1. 各セグメントに 2 つのダイナミック ブロックを作成します。
1. 2 つのダイナミック ブロックを含むブロックを次のように作成 [!DNL Page Builder] ダイナミック ブロック：
1. 上記のブロックを含んだウィジェットを作成し、すべてのページのフッターセクションの下にブロックを表示します。
1. キャッシュをクリアします。
1. ホームページを開きます。
1. 顧客としてログインします。
1. ログアウトします。

<u>期待される結果</u>:

ログインした顧客用に作成されたバナーは、ゲストユーザーには表示されません。

<u>実際の結果</u>:

ログインした顧客セグメント用に作成されたバナーは、顧客アカウントからログアウトした後も表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
