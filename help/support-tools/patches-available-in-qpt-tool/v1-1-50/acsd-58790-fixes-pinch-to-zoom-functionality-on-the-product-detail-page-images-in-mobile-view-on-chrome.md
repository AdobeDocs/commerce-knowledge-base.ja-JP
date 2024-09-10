---
title: 「ACSD-58790：上のモバイル表示の製品詳細ページ画像のピンチからズームの機能を修正  [!DNL Chrome]」
description: ACSD-58790 では、モバイルビューの画像が期待どおりに画像にズームイン  [!DNL Chrome]  なかったAdobe Commerceの問題が修正されました。
feature: Storefront
role: Admin, Developer
source-git-commit: 51c740dc70937c7b80d8492d02ee4a758f103a35
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# ACSD-58790:[!DNL Chrome] のモバイルビューの製品詳細ページ画像のピンチからズームの機能を修正しました

ACSD-58790 パッチは、[!DNL Chrome] のモバイルビューの画像が画像を期待どおりにズームインできなかったAdobe Commerceの問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.50 がインストールされている場合に使用できます。 パッチ ID は ACSD-58790 です。 この問題はAdobe Commerce 2.4.8 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p7

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL Chrome] のモバイルビューの製品詳細ページ画像に対するピンチからズームまでの機能を修正しました。

<u> 再現手順 </u>:

1. 画像付きの製品を作成します。
1. [!DNL Chrome] ブラウザーから製品を開きます。
1. 画像をクリックし、ダブルクリックで画像がズームされることを確認します。
1. [!DNL Chrome] デベロッパーツールを使用して、モバイル表示に切り替えます。
1. 画像をクリックします。
1. ダブルタップします。

<u> 期待される結果 </u>:

画像をダブルクリックすると、ズームインされます。

<u> 実際の結果 </u>:

ダブルクリックしても画像がズームインしない。 [!DNL Firefox] ではズーム機能が期待どおりに動作するので、この問題はモバイル表示の [!DNL Chrome] に固有の問題です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
