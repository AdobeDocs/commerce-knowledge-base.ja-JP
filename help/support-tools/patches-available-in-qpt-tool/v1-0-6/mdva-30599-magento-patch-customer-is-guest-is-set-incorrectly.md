---
title: 「MDVA-30599:customer_is_guest が正しく設定されていません」
description: MDVA-30599 パッチでは、API を使用して作成されたゲストの見積りが、ログインしている顧客の見積りとして誤ってマークされる問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.6 がインストールされている場合に利用できます。 この問題は、Adobe Commerce 2.4.2 で修正されました。
exl-id: e16bb926-241b-451e-89a5-33000f73c5b7
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# MDVA-30599: customer_is_guest が正しく設定されていません

MDVA-30599 パッチでは、API を使用して作成されたゲストの見積りが、ログインしている顧客の見積りとして誤ってマークされる問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.6 がインストールされています。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.4 - 2.4.0

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

API を使用して作成されたゲストの見積が、ログインしている顧客の見積として誤ってマークされます。

<u>再現手順</u>:

1. Adobe Commerce ストアフロントで、商品をゲストユーザーとして買い物かごに追加します。
1. Adobe Commerce DB で、対応するを見つけます `quote_id_mask`.
1. に API リクエストを送信する `quoteGuestCartRepositoryV1` 買い物かご：ゲストの買い物かごのリポジトリーインターフェイス。 Swagger または cURL リクエストを使用して実行できます。

```curl
curl -X GET "http://web2-73.sparta.corp.magento.com/dev/support/ee24dev/rest/all/V1/guest-carts/ToOwPtSBxkorkCLq6ztwupPd99y8zhky" -H "accept: application/json"
```

<u>期待される結果</u>:

応答して、次を取得します `"customer_is_guest": true`

<u>実際の結果</u>:

応答して、次を取得します `"customer_is_guest": false`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## パッチのインストール後に必要な追加手順

このパッチは、すべての新しいゲスト買い物かごに対して有効になります。 既存のゲスト買い物かごを修正する必要がある場合は、を設定します。 `quote.customer_is_guest = 1` 以下の条件を満たすレコード `quote.customer_id` が NULL である。 次のようなクエリを実行できます。

```sql
UPDATE quote SET customer_is_guest = 1 WHERE customer_id IS NULL;
```

>[!WARNING]
>
>実稼動環境で実行する前に、ステージング環境または統合環境でクエリをテストすることを強くお勧めします。 また、DB を使用して操作を行う前に、最新のバックアップを作成することをお勧めします。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
