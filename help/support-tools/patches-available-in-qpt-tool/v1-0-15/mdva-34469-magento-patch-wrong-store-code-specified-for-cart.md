---
title: 「MDVA-34469：買い物かごに指定されたストアコードが正しくありません」
description: 「MDVA-34469 パッチは、ストア表示を切り替えた後に買い物かごに製品を追加すると、「Wrong store code specified for cart*」というエラーメッセージが表示される問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.15 がインストールされている場合に利用できます。 パッチ ID は MDVA-34469。 この問題はAdobe Commerce 2.4.2 で修正されました。'
exl-id: 35d4f120-7fcf-4996-8b23-aca99cfc18ac
feature: Orders, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# MDVA-34469：買い物かごに間違ったストア コードが指定されています

MDVA-34469 パッチを使用すると、ストアの表示を切り替えた後に買い物かごに商品を追加すると、「*買い物かごに指定されたストアコードが正しくありません*」というエラーメッセージが表示される問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.15 がインストールされている場合に使用できます。 パッチ ID は MDVA-34469。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.4.1 - 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストア表示を切り替えようとすると、買い物かごクエリエラー *「買い物かごに指定されたストアコードが正しくありません」* が表示されます。

<u> 前提条件 </u>:

* Adobe Commerce 2.4.0。
* 単一のストアと 2 つのストアビューを持つ単一の web サイトが設定されます。
* 顧客アカウントが作成されます。

<u> 再現手順 </u>:

1. Adobe Commerce バックエンドは、2 つのストアビュー（ストアコード：デフォルト、秒）を持つように設定されています。
1. ユーザーは、デフォルトのストアコードを使用して買い物かごを作成します。
1. ユーザーは、`Store` リクエストヘッダーの 2 番目のストアコードを使用して、この買い物かごを取得しようとします。

<u> 期待される結果 </u>:

買い物かごは、ストアを切り替えると（新しいリクエストヘッダーに新しいコードを送信すると）、`Store` 求されたストアに関連付けられるので、表示されます。

<u> 実際の結果 </u>:

買い物かごクエリがエラーを返し、買い物かごが表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
