---
title: 「ACSD-46988:GraphQL通貨 API リクエストで null 値が返される」
description: ACSD-46988 パッチは、GraphQL通貨 API リクエストがカスタム通貨に対して null 値を返す問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.21 がインストールされている場合に利用できます。 パッチ ID は ACSD-46988 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 8da0ab99-8db9-4222-9400-6df1520267f0
feature: REST, GraphQL
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# ACSD-46988:GraphQL通貨 API リクエストで null 値が返される

ACSD-46988 パッチは、GraphQL通貨 API リクエストがカスタム通貨に対して null 値を返す問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.21 がインストールされています。 パッチ ID は ACSD-46988 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQL通貨 API リクエストが、カスタム通貨に対して null 値を返します。

<u>再現手順</u>:

1. 管理者でカスタム通貨を設定します。 に移動 **システム** > **設定** > **一般** > **通貨設定**.
1. 次のペイロードを持つGraphQL リクエストを送信します。

<pre>
<code class="language-graphql">
{
    currency {
        base_currency_code
        base_currency_symbol
        default_display_currency_code
        default_display_currency_symbol
        available_currency_codes
        exchange_rates {
            currency_to
            rate
        }
    }
}
</code>
</pre>

<u>期待される結果</u>:

このリクエストは、null 値ではなく通貨の値を返します。

<u>実際の結果</u>:

このリクエストは複数の null 値を返します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [品質向上パッチ 「ツール」 > 「使用方法」](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) 『品質向上パッチツール』マニュアルの「」を参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## パッチのインストール後に必要な追加手順

オンプレミス ユーザーの場合：

* 実行： `composer require symfony/intl:"~5.4.11"`

クラウドユーザーの場合：

* 実行： `composer require symfony/intl:"~5.4.11"`
* プッシュ `composer.json` および `composer.lock` ファイルを git リポジトリーに追加し、パッチファイルも追加します。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) 『品質向上パッチツール』マニュアルの
