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

ACSD-51907 パッチは、制限付き管理者ユーザーがオフライン払い戻しによるクレジットメモを作成できないパフォーマンスの問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.33 がインストールされています。 パッチ ID は ACSD-51907 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 &lt; 2.4.3-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

制限付き管理者ユーザーは、オフライン払い戻しを含むクレジット メモを作成できません。

<u>再現手順</u>:

1. を作成 **顧客** （デフォルトの web サイト上）
1. 作成 **新しい web サイト** 関連あり *store* および *ストア表示*.
1. デフォルトの web サイトを新しい web サイトに設定し、キャッシュをクリアします。
1. 顧客構成の変更： **Admin** > **ストア** > **設定** > **顧客** > **顧客設定** > **顧客アカウントの共有= グローバル**.
1. 役割範囲が新しく作成された web サイトに設定された新しい管理者ユーザーロールを作成します *（販売データへのアクセスのみ）* 。対象： **Admin** > **システム** > **権限**.
1. この役割で新しい管理者アカウントを作成します。
1. オンライン支払方法を使用して新しい注文を作成します *（例：Auth.netまたは PayPal）*.
1. 制限付き管理者ユーザーとしてログインします。
1. に移動 **売上** > **注文件数** > then **注文ビューページ**.
1. 請求書を作成します。
1. 「請求書」タブにナビゲートします。
1. クリックする **請求書**.
1. クリックする **[!UICONTROL Credit Memo]**.
1. を確認します **[!UICONTROL Refund to Store Credit]** チェックボックスで、その近くのテキストフィールドを *1* の値。
1. 「」をクリック **[!UICONTROL Refund Offline]** ボタン。

<u>期待される結果</u>:

クレジット・メモが作成され、 *$1* ストア・クレジットに払い戻されます。

<u>実際の結果</u>:

エラーメッセージ *この項目を表示するには、さらに権限が必要です* が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
