---
title: 「ACSD-54887：顧客セッションの有効期限が切れると、顧客の買い物かごがクリアされる」
description: ACSD-54887 パッチを適用すると、[!UICONTROL Persistent Shopping Cart] が有効な状態でカスタマーセッションの有効期限が切れた後に、お客様の買い物かごがクリアされるAdobe Commerceの問題が修正されます。
feature: Shopping Cart
role: Admin, Developer
source-git-commit: fd73d89e8d60f6a4ab2ff5ba08df385adbd3faaa
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---


# ACSD-54887：顧客セッションの有効期限が切れると、顧客の買い物かごがクリアされる

ACSD-54887 パッチは、[!UICONTROL Persistent Shopping Cart] が有効な状態でカスタマーセッションの有効期限が切れた後に、顧客の買い物かごがクリアされる問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.50 がインストールされている場合に使用できます。 パッチ ID は ACSD-54887 です。 この問題はAdobe Commerce 2.4.8 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 ～ 2.4.4-p8、2.4.5-p3 ～ 2.4.5-p7 および 2.4.6-p1 ～ 2.4.6-p5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

顧客の買い物かごは、顧客セッションの有効期限が切れ、[!UICONTROL Persistent Shopping Cart] が有効になるとクリアされます。

<u> 再現手順 </u>:

1. [!UICONTROL Persistent Shopping Cart] を有効にします。 **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Customers]**/**[!UICONTROL Persistent Shopping Cart]**=*はい* に移動します。

   永続性を有効にしてログインします（メモ：ポップアップ認証では使用できませんが、直接 [!UICONTROL Sign in] ページでのみ使用できます）。

1. 商品を買い物かごに追加します。
1. チェックアウトに進み、支払い方法を選択します。
1. セッションを期限切れにします（`PHPSESSID` を削除）。
1. ページを更新します。 支払い方法が既に選択されており、[!UICONTROL Persistent Cart] の Cookie が削除されているので、引用符が即座にゲストの引用符に変換されることを確認します。
1. セッションを期限切れにします（`PHPSESSID` を削除）。
1. ページを更新します。 カートが空であることを確認します。
1. もう一度ログインします。

<u> 期待される結果 </u>:

もう一度ログインすると、買い物かごに製品が表示されます。

<u> 実際の結果 </u>:

再度ログインすると、カートは空になります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。

