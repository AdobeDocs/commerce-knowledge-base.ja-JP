---
title: 「MDVA-42507：買い物かごルールに対してステージング更新を適用した後、完全ページのキャッシュがクリーンアップされる」
description: MDVA-42507 パッチは、買い物かごルールのステージング更新を適用した後に、フルページキャッシュがクリーンアップされる問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.9 がインストールされている場合に利用できます。 パッチ ID は MDVA-42507。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 9303d488-428b-4565-b9ea-469c34856dce
feature: Cache, Categories, Orders, Shopping Cart, Staging
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# MDVA-42507：買い物かごルールに対してステージング更新を適用した後に、完全ページ キャッシュがクリーンアップされる

MDVA-42507 パッチは、買い物かごルールのステージング更新を適用した後に、フルページキャッシュがクリーンアップされる問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.9 がインストールされている場合に使用できます。 パッチ ID は MDVA-42507。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

フルページキャッシュは、買い物かごルールに対してステージング更新を適用した後にクリーンアップされます。

<u> 再現手順 </u>:

1. 開発者モードを有効にします。
1. 複数の製品ページとカテゴリページを開き、（ヘッダーを使用して）キャッシュから読み込まれていることを確認します。
1. 買い物かごルールにステージングの更新を適用します。
1. カテゴリページと製品ページがまだキャッシュから読み込まれているかどうかを確認します。

<u> 期待される結果 </u>:

買い物かごルールに対してステージング更新を適用した後、フルページキャッシュがクリーンアップされない。

<u> 実際の結果 </u>:

フルページキャッシュは、買い物かごルールに対してステージング更新を適用した後にクリーンアップされます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
