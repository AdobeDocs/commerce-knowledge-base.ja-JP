---
title: 「ACSD-51907：制限付き管理者ユーザーは、オフライン払い戻しのクレジットメモを作成できない」
description: ACSD-51907 パッチを適用すると、制限付き管理者ユーザーは、オフライン払い戻しではクレジットメモを作成できないAdobe Commerceの問題を修正できます。
exl-id: 564e8524-f2dc-453c-be78-a920fbd47d71
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# ACSD-51907：制限付き管理者ユーザーは、オフライン払い戻しのクレジット メモを作成できません

ACSD-51907 パッチは、制限付き管理者ユーザーがオフライン払い戻しによるクレジットメモを作成できないパフォーマンスの問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-51907 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 &lt; 2.4.3-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

制限付き管理者ユーザーは、オフライン払い戻しを含むクレジット メモを作成できません。

<u> 再現手順 </u>:

1. デフォルトの web サイトに **顧客** を作成します。
1. 関連する **ストア** および *ストア表示* を使用して *新しい web サイト* を作成します。
1. デフォルトの web サイトを新しい web サイトに設定し、キャッシュをクリアします。
1. 顧客設定を変更：**管理者**/**ストア**/**設定**/**顧客**/**顧客設定**/**顧客アカウントを共有= グローバル**
1. **管理者**/**システム**/**権限** で、役割の範囲を新しく作成された web サイト *（販売データへのアクセスのみ）* 設定した新しい管理者ユーザーロールを作成します。
1. この役割で新しい管理者アカウントを作成します。
1. オンライン支払い方法 *（例：Auth.netまたは PayPal）* を使用して新しい注文を作成します。
1. 制限付き管理者ユーザーとしてログインします。
1. **Sales**/**Orders**/**order view page** に移動します。
1. 請求書を作成します。
1. 「請求書」タブにナビゲートします。
1. **請求書** をクリックします。
1. 「**[!UICONTROL Credit Memo]**」をクリックします。
1. 「**[!UICONTROL Refund to Store Credit]**」チェックボックスをオンにして、その近くのテキストフィールドを *1* 値に設定します。
1. 「**[!UICONTROL Refund Offline]**」ボタンをクリックします。

<u> 期待される結果 </u>:

クレジットメモが作成され、*$1* が店舗クレジットに払い戻されます。

<u> 実際の結果 </u>:

*この項目を表示するには、さらに権限が必要です* というエラーメッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
