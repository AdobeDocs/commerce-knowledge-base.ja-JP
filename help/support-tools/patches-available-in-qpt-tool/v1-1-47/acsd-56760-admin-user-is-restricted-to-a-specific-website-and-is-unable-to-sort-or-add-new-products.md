---
title: 「ACSD-56760：管理者ユーザーが特定の web サイトに制限されており、新しい製品を並べ替えまたは追加できない」
description: ACSD-56760 パッチを適用すると、特定の web サイトに制限されている管理者ユーザーが、web ストアに独自のルートカテゴリがある場合、カテゴリ内で新しい商品の並べ替えや追加ができないAdobe Commerceの問題を修正できます。
role: Admin
exl-id: fc1898ce-dcd7-4c0b-bef0-445219e8455f
source-git-commit: a8e1b3b5b9de41c62bf819ef68ac9f89626483a1
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# ACSD-56760：管理者ユーザーが特定の web サイトに制限されており、新しい製品を並べ替えたり追加したりすることができません

ACSD-56760 パッチは、特定の web サイトに制限されている管理者ユーザーが、web ストアに独自のルートカテゴリがある場合に、カテゴリ内で新しい製品の並べ替えや追加ができない問題を修正しました。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.47 がインストールされています。 パッチ ID は ACSD-56760 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーが特定の web サイトに限定されており、web ストアに独自のルートカテゴリがある場合に、カテゴリ内で新しい製品を並べ替えたり追加したりできない。

<u>再現手順</u>:

1. 作成 *2* web サイト。
1. を作成 **[!UICONTROL restricted admin user]** アクセス権がのみ *1* web サイト。
1. としてログイン **[!UICONTROL restricted admin user]** カテゴリ内の製品の位置を変更してみてください。

*ケース 1*:

* *2* ストア。
* *2* ルートカテゴリ（各 web サイトに割り当てられた独自のカテゴリルート）。

*ケース 2*:

* *2* ストア。
* のみ *1* ルートカテゴリは両方の web サイトに割り当てられます。

<u>期待される結果</u>:

* *ケース 1*：制限付き管理者は、利用可能なカテゴリ内の製品を並べ替えることができるはずです。
* *ケース 2*：制限された管理者は、使用可能なカテゴリ内の製品を並べ替えることはできません。これは、制限されたストアにも影響を与えるからです。

<u>実際の結果</u>:

* *ケース 1*：制限付き管理者は、利用可能なカテゴリ内の製品を並べ替えることができません。
* *ケース 2*：制限付き管理者は、利用可能なカテゴリ内の製品を並べ替えることができ、制限付きストアに影響します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
