---
title: 「ACSD-52906：ログインしたカスタマーキャッシングに関する X-Magento-Vary Cookie の問題の解決」
description: ログイン中のお客様の X-Magento変更 Cookie が正しく設定されないAdobe Commerceの問題を修正するには、ACSD-52906 パッチを適用してください。
feature: Cache
role: Admin, Developer
exl-id: 863e0808-9208-467d-8d56-9dd7a7f4354d
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# ACSD-52906：ログイン済みのお客様の X-Magentoー変化 Cookie の問題の解決

ACSD-52906 パッチは、ログインしているお客様に対して X-Magento変数 Cookie が正しく設定されない問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.36 がインストールされている場合に使用できます。 パッチ ID は ACSD-52906 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

X-Magento変数 cookie が、同じカスタマーセグメントに属するログイン済みユーザーに対して正しく設定されておらず、一部のページで不適切なキャッシュが発生します。

<u> 前提条件 </u>:

Adobe Commerce Inventory management（MSI）モジュールがインストールされ、有効になっています。

<u> 再現手順 </u>:

1. [!DNL Varnish] または [!DNL Fastly] キャッシュを設定します。
1. 新しい顧客セグメントを作成して、（登録済み *顧客* に割り当てます。
1. customer1 と customer2 のように、2 つの顧客を作成します。
1. キャッシュをクリアします。
1. customer1 としてログインし、ホームページに移動します。
1. ブラウザーで匿名ページを開きます。
1. ホーム ページ以外の任意のページに移動します。
1. customer2 としてログインします。
1. ホームページに移動します。
1. ページがブラウザー開発コンソールにキャッシュされているかどうかを確認します。

<u> 期待される結果 </u>:

ページがキャッシュから取得されます。

<u> 実際の結果 </u>:

ページはキャッシュされません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
