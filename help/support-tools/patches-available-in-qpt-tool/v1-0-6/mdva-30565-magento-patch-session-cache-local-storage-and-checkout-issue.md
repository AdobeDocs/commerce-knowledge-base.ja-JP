---
title: 「MDVA-30565：セッションキャッシュのローカルストレージとチェックアウトの問題」
description: MDVA-30565 パッチは、セッションキャッシュのローカルストレージとチェックアウトの問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.6 がインストールされている場合に利用できます。
exl-id: f0693f0c-fc6b-44af-a6a0-ebfa973bca65
feature: Cache, Checkout, Orders, Storage
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# MDVA-30565: セッション キャッシュのローカル ストレージとチェックアウトの問題

MDVA-30565 パッチは、セッションキャッシュのローカルストレージとチェックアウトの問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.6 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.3.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

買い物かごの項目は、顧客セッションがタイムアウトした際にも、買い物かごページに表示できます。 これにより、ゲストのチェックアウトに使用できる発送方法がない、推定発送方法エラーが発生します。

<u>再現手順</u>:

1. Commerce Admin で永続的な買い物かごを有効にします。 （**永続性を有効にする** = &quot;*はい*``）
1. フロントエンドで顧客としてログインします。 これにより、 `persistent_shopping_cart` cookie を使用し、永続的なセッションを開始します。
1. 商品を買い物かごに追加します。
1. フロントエンドセッションがタイムアウトするまで待つか、 `PHPSESSID` cookie。
1. ゲストユーザーになっていますが、買い物かごに移動すると、ログインした顧客として追加された製品を引き続き表示できます。
1. 買い物かごから製品を削除すると、買い物かごが空になります。 Adobe Commerceがを削除しているのがわかります `persistent_shopping_cart` このイベントの cookie。
1. 新しい商品を買い物かごに追加し、買い物かごページに移動します。
1. ブラウザーコンソールに表示されます。 `V1/guest-carts/4/estimate-shipping-methods` リクエストは、メッセージを含む 404 応答を返すようになりました `{"message":"No such entity        with %fieldName = %fieldValue","parameters":{"fieldName":"cartId","fieldValue":0}}`

<u>期待される結果</u>:

出荷方法の見積もりリクエストが正しい結果を返します。

<u>実際の結果</u>:

推定発送方法リクエストが次のようなエラーで失敗します。*申し訳ありませんが、現在この注文で利用できる見積もりはありません。*“

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
