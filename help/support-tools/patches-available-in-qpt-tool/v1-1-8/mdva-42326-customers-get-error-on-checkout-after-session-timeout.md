---
title: 「MDVA-42326：セッションタイムアウト後、チェックアウト時にエラーが発生する」
description: MDVA-42326 パッチは、永続ショッピング カートが有効になっている場合でも、セッション タイムアウト後にチェックアウト時に顧客にエラーが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.8 がインストールされている場合に利用できます。 パッチ ID は MDVA-42326。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: bc9b71de-510d-4c4e-8b0d-9abf9a3e447f
feature: Checkout, Orders
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# MDVA-42326：セッションタイムアウト後、チェックアウト時にエラーが発生する

MDVA-42326 パッチは、永続ショッピング カートが有効になっている場合でも、セッション タイムアウト後にチェックアウト時に顧客にエラーが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.8 がインストールされている場合に使用できます。 パッチ ID は MDVA-42326。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.6 ～ 2.3.7-p2、2.4.1 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

永続買い物かごが有効になっている場合でも、セッションタイムアウト後のチェックアウトでエラーが発生します。

<u> 前提条件 </u>:

1. **Config**/**General**/**Web**/**Default Cookie Settings**/**Cookie Lifetime** に移動して、**120** に設定します。
1. **Config**/**Customers**/**Customer Configuration**/**Online Customers Options** に移動し、両方の値を **2** に設定します。
1. **Config**/**顧客**/**永続的な買い物かご** に移動し、**有効** に設定します。
1. **Config**/**Sales**/**Payment Methods** に移動し、**Check/Money Order** 以外のすべての支払い方法をオフにします（有効にする必要があります）。

<u> 再現手順 </u>:

1. 顧客としてログインし、いくつかの製品を買い物かごに追加します。
1. 買い物かごを確認します。
1. 2 分待ちます（事前条件で設定）。セッションはタイムアウトします。
1. **チェックアウトに移動** をクリックし、ページを更新しないでください。
1. ゲストとしてチェックアウトし、配送先住所を入力して、配送方法を選択します。
1. **次へ** をクリックします。
1. **レビューと支払い** ページで、「注文 **をクリック** します。 お支払い方法は 1 つのみなので、お客様は支払い方法を選択せずに注文できる必要があります。

<u> 期待される結果 </u>:

お客様が注文できるはずです。

<u> 実際の結果 </u>:

*アドレス検証に失敗しました：メールの形式が間違っています* というエラーが発生する。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
