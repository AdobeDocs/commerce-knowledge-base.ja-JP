---
title: 「MDVA-34867：スケジュール済み更新の条件フィールドセット値が保存されない」
description: MDVA-34867 パッチは、カタログ価格ルールを編集する際に、新しいスケジュール更新内の条件の値が保存されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.17 がインストールされている場合に利用できます。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: bf514ccc-bebd-4ed2-868f-28b02b1e253e
feature: Catalog Management, Categories
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# MDVA-34867：スケジュール済み更新の条件フィールドセット値が保存されない

MDVA-34867 パッチは、カタログ価格ルールを編集する際に、新しいスケジュール更新内の条件の値が保存されない問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.17 がインストールされています。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.4.0-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カタログ価格ルールを編集する際に、新しいスケジュール更新の条件の値が保存されません。

<u>再現手順</u>:

1. 管理者にログインします。
1. を作成 **カタログルール** （を使用） **条件** = &quot;*カテゴリは 1 です*」と入力します。
1. 開始日が将来の更新（例：明日）をスケジュールして **条件** = &quot;*カテゴリは 2、3 です*」を選択して、更新を保存します。
1. クリックする **表示/編集** 上記で作成した更新の場合は、条件フィールドを確認します。

<u>期待される結果</u>:

この **カタログルール**  **条件** = &quot;*カテゴリは 2、3 です*」と入力します。

<u>実際の結果</u>:

この **カタログルール**  **条件** = &quot;*カテゴリは 1 です*」が表示されます。これは、更新が保存されなかったことを意味します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
