---
title: 「ACSD-46618：製品リストウィジェットに、ログインした顧客のキャッシュされた価格が正しく表示されない」
description: ログインしているお客様の商品リストウィジェットに誤ったキャッシュ価格が表示されるAdobe Commerceの問題を修正するために、パッチを適用します。
exl-id: 8b182822-1d3d-4793-871b-cdf4565d0712
feature: Cache, Orders, Products
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# ACSD-46618：製品リストウィジェットに、ログインした顧客に対して正しくないキャッシュ価格が表示される

ACSD-46618 パッチを使用すると、ログインしている顧客の製品リストウィジェットに誤ったキャッシュ価格が表示される問題を解決できます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/announcements/commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.html) 1.1.21 がインストールされています。 パッチ ID は ACSD-46618 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ACSD-46618 パッチを使用すると、ログインしている顧客の製品リストウィジェットに誤ったキャッシュ価格が表示される問題を解決できます。

<u>再現手順</u>:

1. Adobe Commerce Admin で、次を選択します。 **[!UICONTROL Stores]**、次に **[!UICONTROL Configuration]**、を展開 **[!UICONTROL Sales]**&#x200B;を選択し、 **[!UICONTROL Tax]**. 税金設定を更新して、税金を含む価格と税金を除外する価格を表示します。
1. を設定 **[!UICONTROL Enable Cross Border Trade]** = _はい_.
1. 米国にのみ適用される税務処理基準を作成します。
1. 複数の製品を含むホームページにウィジェットを追加します。
1. 米国住所と米国以外の住所を持つ 2 つの顧客を作成します。
1. ストアフロントから米国の顧客を使用してログインします。 ページがキャッシュされていることを確認します。
1. ホームページウィジェットに表示される価格を確認します。
1. 米国以外のお客様がログアウトしてログインします。

<u>期待される結果</u>:

ホームページウィジェットに表示される価格は、顧客の住所に対応しています。

<u>実際の結果</u>:

ホームページ ウィジェットには、米国以外の顧客の価格が税金を使用して表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、次を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
