---
title: 「MDVA-42855：チェックアウト時に、新しい顧客アドレスがアドレス帳に保存されない」
description: MDVA-42855 パッチを適用すると、チェックアウト時に新しい顧客アドレスがアドレス帳に保存されない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-42855。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 37fc51f4-773e-4bef-9fb1-e6629562b94a
feature: Checkout, Orders, Shipping/Delivery
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# MDVA-42855：チェックアウト時に新しい顧客アドレスがアドレス帳に保存されない

MDVA-42855 パッチを適用すると、チェックアウト時に新しい顧客アドレスがアドレス帳に保存されない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.12 がインストールされている場合に使用できます。 パッチ ID は MDVA-42855。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

チェックアウト時に、新しい顧客の住所はアドレス帳に保存されません。

<u> 再現手順 </u>:

1. 顧客アカウントを作成し、デフォルトの配送先住所と請求先住所を更新します。
1. 買い物かごに商品を追加し、チェックアウトページに移動します。
1. [ 配送先 ] で、[**+新しい住所**] をクリックします。
1. 新しいアドレスを入力し、「**アドレス帳に保存**」チェックボックスをオンのままにします。
1. 「支払い」で、「**請求先と配送先住所が同じです**」チェックボックスにチェックマークを入れます。
1. 注文します。
1. アドレス帳を調べなさい。

<u> 期待される結果 </u>:

新しい配送先住所がアドレス帳に保存されます。

<u> 実際の結果 </u>:

新しい配送先住所はアドレス帳に保存されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
