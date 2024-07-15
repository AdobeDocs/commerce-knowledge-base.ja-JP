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

MDVA-30599 パッチでは、API を使用して作成されたゲストの見積りが、ログインしている顧客の見積りとして誤ってマークされる問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.6 がインストールされている場合に使用できます。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.4 - 2.4.0

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

API を使用して作成されたゲストの見積が、ログインしている顧客の見積として誤ってマークされます。

<u> 再現手順 </u>:

1. Adobe Commerce ストアフロントで、商品をゲストユーザーとして買い物かごに追加します。
1. Adobe Commerce DB で、対応する `quote_id_mask` を見つけます。
1. ゲスト買い物かごの買い物かごリポジトリインターフェイス `quoteGuestCartRepositoryV1`API リクエストを送信します。 Swagger または cURL リクエストを使用して実行できます。

```curl
curl -X GET "http://web2-73.sparta.corp.magento.com/dev/support/ee24dev/rest/all/V1/guest-carts/ToOwPtSBxkorkCLq6ztwupPd99y8zhky" -H "accept: application/json"
```

<u> 期待される結果 </u>:

それに応じて、あなたは `"customer_is_guest": true` を得る

<u> 実際の結果 </u>:

それに応じて、あなたは `"customer_is_guest": false` を得る

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## パッチのインストール後に必要な追加手順

このパッチは、すべての新しいゲスト買い物かごに対して有効になります。 既存のゲスト買い物かごを修正する必要がある場合、`quote.customer_id` が NULL であるレコードの `quote.customer_is_guest = 1` を設定します。 次のようなクエリを実行できます。

```sql
UPDATE quote SET customer_is_guest = 1 WHERE customer_id IS NULL;
```

>[!WARNING]
>
>実稼動環境で実行する前に、ステージング環境または統合環境でクエリをテストすることを強くお勧めします。 また、DB を使用して操作を行う前に、最新のバックアップを作成することをお勧めします。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
