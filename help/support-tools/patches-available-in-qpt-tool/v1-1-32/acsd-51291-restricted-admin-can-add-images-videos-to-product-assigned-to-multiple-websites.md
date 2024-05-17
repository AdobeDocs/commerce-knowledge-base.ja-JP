---
title: 「ACSD-51291：制限付き管理者が、複数の web サイトに割り当てられた製品に画像/ビデオを追加できる」
description: ACSD-51291 パッチを適用すると、1 つの web サイトへのアクセスを制限された管理者が、複数の web サイトに割り当てられた製品に画像/ビデオを追加できるAdobe Commerceの問題を修正できます。
feature: Admin Workspace, Products, Page Content
role: Admin
exl-id: d3cf5009-6b80-4841-95c3-75bb15c9c0a4
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# ACSD-51291：制限付き管理者は、複数の web サイトに割り当てられた製品に画像/ビデオを追加できる

ACSD-51291 パッチは、1 つの web サイトへのアクセスを持つ制限付き管理者が、複数の web サイトに割り当てられた製品に画像/ビデオを追加できる問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.32 がインストールされています。 パッチ ID は ACSD-51291 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 ～ 2.4.4-p3、2.4.5 ～ 2.4.5-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

1 つの web サイトへのアクセス権を持つ制限付き管理者は、複数の web サイトに割り当てられた製品に画像/ビデオを追加できます。

<u>再現手順</u>

1. 管理者としてログインします。
1. 2 つ目の web サイト、ストア、ストア表示を作成します。
1. 2 つ目の web サイト、ストア、ストアの各表示用のリソースのみを持つ 2 つ目の管理者ロールを作成します。
1. 2 人目の管理者を作成して、新しい制限付き管理者の役割に割り当てます。
1. 新しい製品を作成して、デフォルトの Web サイトと新しい Web サイトの両方に割り当てます。
1. メインの管理プロファイルからログアウトします。
1. 新しい制限付き管理者としてログインします。
1. 両方の web サイトに割り当てられている、作成した製品を編集します。
1. を開きます **[!UICONTROL Images and Videos]** タブ。

<u>期待される結果</u>:

* 次のメッセージが表示されます。

  *制限付き管理者は、製品が割り当てられているすべての web サイトに対する権限を管理者が持っている場合にのみ、画像やビデオでアクションを実行できます。*

* この **[!UICONTROL Add Video]** ボタンがアクティブではありません。

<u>実際の結果</u>:

制限付き管理者は、アクセス権のない web サイトに製品が割り当てられている場合でも、画像やビデオを追加できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
