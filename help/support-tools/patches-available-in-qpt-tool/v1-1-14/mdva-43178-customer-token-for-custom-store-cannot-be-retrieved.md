---
title: 「MDVA-43178：カスタムストアのカスタムトークンをGraphQLで取得できない」
description: MDVA-43178 パッチでは、カスタムストアのカスタムトークンをGraphQLで取得できない問題を修正しています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.14 がインストールされている場合に利用できます。 パッチ ID は MDVA-43178。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: b2a8bf96-7534-41d2-b83b-58d8e0b6d076
feature: GraphQL
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# MDVA-43178: GraphQLでカスタム ストアの顧客トークンを取得できません

MDVA-43178 パッチでは、カスタムストアのカスタムトークンをGraphQLで取得できない問題を修正しています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.14 がインストールされています。 パッチ ID は MDVA-43178。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1 - 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カスタムストアのカスタムトークンは、GraphQLで取得できません。

<u>再現手順</u>:

1. デフォルトストアに対して 2 つのストア表示を作成します。
1. 新しい Web サイト、1 つのストア、1 つのストアビューを作成します。 このストア表示に「test3」という名前を付けます。
1. 新しい web サイトの顧客を作成します。
1. API 管理トークンを生成：

   `http://domain/rest/all/V1/integration/admin/token`

   <pre>
    <code class="language-graphql">
    {
      "username": "login",
      "password": "password"
    }
    </code>
    </pre>

1. GraphQLを送信して、管理者としてカスタマートークンを取得します。認証には管理者トークンを使用します。ヘッダーには「store」 = 「test3」と記載されています。

   <pre>
    <customer_email>
      </pre>

<u>期待される結果</u>:

顧客トークンが生成されます。

<u>実際の結果</u>:

顧客トークンが生成されていません。 商人は得る *提供された顧客の E メールは存在しません* それに応えて。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
