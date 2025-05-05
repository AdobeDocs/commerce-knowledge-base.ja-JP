---
title: 「ACSD-57588：複数のアドレスに送信する際に、地域 ID 処理でエラーが発生しました」
description: ACSD-57588 パッチを適用すると、リージョン ID の処理中に複数のアドレスに注文を送信するとエラーがトリガーされるAdobe Commerceの問題を修正できます。
feature: Orders, Shipping/Delivery
role: Admin, Developer
source-git-commit: 1899e4601d292a8543d1c34e622251a7f6aed124
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# ACSD-57588：複数のアドレスに送信する際に、地域 ID 処理でエラーが発生しました

ACSD-57588 パッチでは、複数のアドレスに注文を送信すると、リージョン ID の処理中にエラーがトリガーする問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.49 がインストールされている場合に使用できます。 パッチ ID は ACSD-57588 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数のアドレスに送信する場合、地域 ID の処理中にエラーがトリガーされます。

<u> 再現手順 </u>:

1. [!DNL Braintree] の支払方法を設定します。
1. ストアフロントで顧客としてログインします。
1. 買い物かごに製品を追加し、買い物かごを表示して編集する手順に進みます。
1. チェックアウトプロセス中に複数の住所 *（例：英国、米国* CA）を追加し、注文を確認します。
1. チェックアウトページで、クレジットカード支払いオプションを選択し、必要な資格情報を入力して注文します。

<u> 期待される結果 </u>:

注文は正常に行えます。

<u> 実際の結果 </u>:

注文は行われません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
