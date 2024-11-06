---
title: 「MDVA-42509：クイックオーダーの CSV をアップロードできず、「Cookie を送信できません」というエラーが発生する」
description: MDVA-42509 パッチは、クイックオーダー用に CSV をアップロードできなかった結果、「Cookie を送信できません」というエラーが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.16 がインストールされている場合に利用できます。 パッチ ID は MDVA-42509。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 7aa0e710-9a28-4531-b9cb-c82f654487f4
feature: B2B, Orders
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# MDVA-42509: クイック注文で CSV をアップロードできず、「Cookie を送信できません」というエラーが発生する

MDVA-42509 パッチは、クイックオーダーで CSV をアップロードできなかった結果として *Cookie を送信できません* というエラーが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.16 がインストールされている場合に使用できます。 パッチ ID は MDVA-42509。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

CSV を使用して多数の製品でクイックオーダーを作成すると、cookie エラー *cookie を送信できません* が表示されます

<u> 再現手順 </u>:

1. **ストア**/**設定**/**設定**/**一般**/**B2B 機能** に移動して、クイックオーダーを有効にします。
1. 顧客アカウントを作成し、上部のリンクにある **クイックオーダー** に移動します。
1. 100 を超える SKU を持つ CSV を使用して、クイックオーダーを作成してみてください。

<u> 期待される結果 </u>:

多数の SKU を使用してクイックオーダーを作成できます。

<u> 実際の結果 </u>:

cookie のサイズに関連したエラーメッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
