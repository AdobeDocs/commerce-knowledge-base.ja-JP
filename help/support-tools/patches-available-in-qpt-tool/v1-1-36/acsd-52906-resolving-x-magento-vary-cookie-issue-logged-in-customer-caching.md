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

ACSD-52906 パッチは、ログインしているお客様に対して X-Magento変数 Cookie が正しく設定されない問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.36 がインストールされています。 パッチ ID は ACSD-52906 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

X-Magento変数 cookie が、同じカスタマーセグメントに属するログイン済みユーザーに対して正しく設定されておらず、一部のページで不適切なキャッシュが発生します。

<u>前提条件</u>:

Adobe Commerce Inventory management（MSI）モジュールがインストールされ、有効になっています。

<u>再現手順</u>:

1. 設定 [!DNL Varnish] または [!DNL Fastly] キャッシュ。
1. 新しい顧客セグメントを作成して、に割り当てます *登録済み* 顧客。
1. customer1 と customer2 のように、2 つの顧客を作成します。
1. キャッシュをクリアします。
1. customer1 としてログインし、ホームページに移動します。
1. ブラウザーで匿名ページを開きます。
1. ホーム ページ以外の任意のページに移動します。
1. customer2 としてログインします。
1. ホームページに移動します。
1. ページがブラウザー開発コンソールにキャッシュされているかどうかを確認します。

<u>期待される結果</u>:

ページがキャッシュから取得されます。

<u>実際の結果</u>:

ページはキャッシュされません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
