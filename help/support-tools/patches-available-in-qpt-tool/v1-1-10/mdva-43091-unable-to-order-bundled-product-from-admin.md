---
title: 「MDVA-43091：管理者からバンドル製品を注文できない」
description: MDVA-43091 パッチを適用すると、Commerce Admin からバンドル製品を注文できない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.10 がインストールされている場合に利用できます。 パッチ ID は MDVA-43091。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 77dff356-4f75-4b06-b62b-5379a4eec273
feature: Admin Workspace, Orders, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# MDVA-43091：管理者からバンドル製品を注文できない

MDVA-43091 パッチを適用すると、Commerce Admin からバンドル製品を注文できない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.10 がインストールされている場合に使用できます。 パッチ ID は MDVA-43091。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者からバンドルされた製品を注文しようとすると、次のエラーがスローされます。*この製品では 10 進数の数量を使用できません。*

<u> 再現手順 </u>:

1. クリーンなAdobe Commerceをインストールします。
1. 2 つのシンプルな製品を作成します。
1. 2 つのオプションを備えたバンドル製品を作成します。
1. フロントエンドで顧客アカウントを作成します。
1. **Admin**/**Sales**/**Orders**/**Create New Order** に移動します。
   * 作成したばかりの顧客アカウントを選択します。
   * バンドルされた製品を買い物かごに追加してみてください。

<u> 期待される結果 </u>:

管理者ユーザーは、1 つの数量を持つ製品を買い物かごに追加できます。

<u> 実際の結果 </u>:

管理者ユーザーに次のエラーが表示されます。*この製品では 10 進数の数量を使用できません。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
