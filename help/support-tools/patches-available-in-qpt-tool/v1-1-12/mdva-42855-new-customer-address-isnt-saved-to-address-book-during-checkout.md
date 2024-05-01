---
title: 「MDVA-42855：チェックアウト時に、新しい顧客アドレスがアドレス帳に保存されない」
description: MDVA-42855 パッチを適用すると、チェックアウト時に新しい顧客アドレスがアドレス帳に保存されない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-42855。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 37fc51f4-773e-4bef-9fb1-e6629562b94a
feature: Checkout, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# MDVA-42855：チェックアウト時に新しい顧客アドレスがアドレス帳に保存されない

MDVA-42855 パッチを適用すると、チェックアウト時に新しい顧客アドレスがアドレス帳に保存されない問題が修正されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-42855。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

チェックアウト時に、新しい顧客の住所はアドレス帳に保存されません。

<u>再現手順</u>:

1. 顧客アカウントを作成し、デフォルトの配送先住所と請求先住所を更新します。
1. 買い物かごに商品を追加し、チェックアウトページに移動します。
1. 「出荷」で、をクリックします。 **+新しいアドレス**.
1. 新しいアドレスを入力し、 **アドレス帳に保存** チェックボックスがオンになっています。
1. 支払い時に、 **請求先と配送先住所が同じです** チェックボックス。
1. 注文します。
1. アドレス帳を調べなさい。

<u>期待される結果</u>:

新しい配送先住所がアドレス帳に保存されます。

<u>実際の結果</u>:

新しい配送先住所はアドレス帳に保存されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
