---
title: 「ACSD-48784：顧客グループ間で顧客セグメント価格が正しくキャッシュされない」
description: ACSD-48784 パッチを適用すると、顧客セグメント価格が顧客グループ間で誤ってキャッシュされるAdobe Commerceの問題を修正できます。
exl-id: 6be11fd0-5c93-4ac7-8664-7e2a289c9e38
feature: Admin Workspace, Cache, Customer Service, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# ACSD-48784：顧客グループ間で顧客セグメント価格が正しくキャッシュされない

ACSD-48784 パッチは、顧客セグメント価格が顧客グループ間で誤ってキャッシュされる問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされている場合に使用できます。 パッチ ID は ACSD-48784 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

顧客セグメント価格が、顧客グループ間で正しくキャッシュされません。

<u> 前提条件 </u>:

[!DNL Varnish] または [!DNL Fastly] を設定します。

<u> 再現手順 </u>:

1. ストアでフルページキャッシュを有効にします。
1. 特別な顧客グループ価格のユーザーとしてサイトにログインします。
1. お客様グループ向けの特別価格の製品については、製品ページに移動してください。 *特別価格* を確認します。
1. 別のブラウザーで、ログインせずにゲストユーザーと同じ製品ページを開きます。 通常の価格を確認してください。
1. Adobe Commerce管理インターフェイスにアクセスし、このストアのAdobe Commerceと [!DNL Fastly] キャッシュをクリアします。
1. ログインブラウザーで、`X-Magento-Vary` の Cookie を削除します。
1. ログインブラウザーで、キャッシュが完全にフラッシュされるまで、同じ製品ページを何度かリロードします。
1. ログインしていないブラウザーで製品ページをリロードして、顧客グループの価格を表示します。

<u> 期待される結果 </u>:

製品ページには、特定の顧客グループに対する正しい価格が表示されます。

<u> 実際の結果 </u>:

* ゲストユーザーには、特別なログインユーザー料金が表示されます。
* 製品が追加されると、ミニカートには正しい価格が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
