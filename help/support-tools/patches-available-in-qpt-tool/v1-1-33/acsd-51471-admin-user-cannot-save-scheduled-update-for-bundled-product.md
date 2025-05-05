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

ACSD-51471 パッチは、管理者ユーザーが、スケジュールされた更新で単純な製品を使用するバンドル製品のスケジュールされた更新を保存できない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-51471 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーは、バンドル製品自体にスケジュール済みアップデートがある単純な製品を使用している場合、スケジュール済みアップデートを保存することはできません。

<u> 再現手順 </u>:

1. シンプルな製品を作成します。
1. *開始日* のみで *終了日* のないシンプル製品のスケジュール済み更新を追加します。
1. アップデート適用後に、商品の SKU を変更します。
1. バンドルされた製品を作成し、手順 1 で作成したシンプルな製品を子製品として追加します。
1. バンドルされた製品を有効にするには、バンドルされた製品のスケジュールされたアップデートを作成します。 スケジュールされている更新の *開始日* と *終了日* の両方を指定します。
1. スケジュールされた更新を保存します。

<u> 期待される結果 </u>:

スケジュールされた更新は正常に保存されました。

<u> 実際の結果 </u>:

スケジュールされた更新を保存すると、次のエラーが発生します。*リクエストされた製品が存在しません。 製品を確認して、もう一度試してください。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
