---
title: 「ACSD-50815：新しいバンドル製品オプションでは、単純製品の 10 進数の数量を使用できない」
description: ACSD-50815 パッチを適用すると、新しいバンドル製品オプションで単純製品の 10 進数の数量が使用できないAdobe Commerceの問題を修正できます。
feature: Products
role: Admin
exl-id: f4aa417c-b0eb-4a68-bf1e-fd86770cc72d
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# ACSD-50815：新しいバンドル製品オプションでは、単純製品の 10 進数の数量を使用できません

ACSD-50815 パッチでは、新しいバンドル製品オプションに単純な製品の 10 進数の数量を使用できない問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.35 がインストールされています。 パッチ ID は ACSD-50815 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

新しいバンドル製品オプションでは、単純な製品の 10 進数の数量を使用できません。

<u>再現手順</u>:

1. 管理者としてログインします。
1. シンプルな製品を新規作成します。
   * が含まれる **[!UICONTROL Advanced Inventory]** ウィンドウ、設定#ウインドウ セッテイ# [!UICONTROL Qty Uses Decimal] = [!UICONTROL Yes].
   * シンプルな製品を保存します。
1. 新しいバンドル製品を作成します。
1. 任意のオプションを追加します。
1. このオプションにシンプルな製品を追加します。
1. バンドルされた商品オプションで、シンプルな商品の 10 進数の数量を設定します。 例えば、1.5 と指定します。

<u>期待される結果</u>:

10 進数の数量を設定できます。 エラーは表示されません。

<u>実際の結果</u>:

エラー： *このフィールドに有効な数値を入力してください* が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
