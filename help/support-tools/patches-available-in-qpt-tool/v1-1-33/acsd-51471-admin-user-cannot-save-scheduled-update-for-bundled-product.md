---
title: 「ACSD-51471：管理者ユーザーは、バンドルされた製品のスケジュールされた更新を保存できない」
description: ACSD-51471 パッチを適用すると、管理者ユーザーが、スケジュールされたアップデートで単純な製品を使用するバンドル製品のスケジュールされたアップデートを保存できないAdobe Commerceの問題を修正できます。
exl-id: 7d80aef0-8505-4491-bde3-5b1a30b840f6
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# ACSD-51471：管理者ユーザーが、バンドルされた製品のスケジュールされた更新を保存できない

ACSD-51471 パッチは、管理者ユーザーが、スケジュールされた更新で単純な製品を使用するバンドル製品のスケジュールされた更新を保存できない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされています。 パッチ ID は ACSD-51471 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーは、バンドル製品自体にスケジュール済みアップデートがある単純な製品を使用している場合、スケジュール済みアップデートを保存することはできません。

<u>再現手順</u>:

1. シンプルな製品を作成します。
1. シンプル製品のスケジュールされた更新を、のみで追加します *開始日* と、なし *終了日*.
1. アップデート適用後に、商品の SKU を変更します。
1. バンドルされた製品を作成し、手順 1 で作成したシンプルな製品を子製品として追加します。
1. バンドルされた製品を有効にするには、バンドルされた製品のスケジュールされたアップデートを作成します。 両方を指定 *開始日* および *終了日* （スケジュールされた更新）。
1. スケジュールされた更新を保存します。

<u>期待される結果</u>:

スケジュールされた更新は正常に保存されました。

<u>実際の結果</u>:

スケジュールされた更新を保存すると、次のエラーが発生します。 *リクエストされた商品は存在しません。 製品を確認して、もう一度試してください。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
