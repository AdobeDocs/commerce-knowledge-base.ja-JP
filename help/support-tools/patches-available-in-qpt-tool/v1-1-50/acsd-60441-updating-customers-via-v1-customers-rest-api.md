---
title: 「ACSD-60441:V1/customers [!DNL REST] API エンドポイントを介して顧客を更新すると、エラーがスローされる」
description: ACSD-60441 パッチを適用すると、バックエンドから生成された統合アクセストークンを使用する際に V1/customers [!DNL REST] API 経由でお客様をアップデートするとエラーがスローされるAdobe Commerceの問題を修正できます。
feature: REST, Customers
role: Admin, Developer
source-git-commit: ea62d2387ab0c04fe44291df431f42d78a0d2f2a
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# ACSD-60441:[!DNL REST] API エンドポイントを介して顧客 `V1/customers` 更新すると、エラーがスローされる

ACSD-60441 パッチでは、バックエンドから生成された統合アクセストークン `V1/customers` 使用する際に [!DNL REST] API を介して顧客を更新するとエラーが発生する問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.50 がインストールされている場合に使用できます。 パッチ ID は ACSD-60441 です。 この問題はAdobe Commerce 2.4.8 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p8

**Adobe Commerce バージョンとの互換性**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p9、2.4.5-p8、2.4.6-p6、2.4.7-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

バックエンドから生成され `V1/customers` 統合アクセストークンを使用する際に [!DNL REST] API エンドポイントを介して顧客を更新すると、エラーがスローされる。

<u> 再現手順 </u>:

1. 管理者から統合を作成します。
1. 統合トークンを使用して、`rest/default/V1/customers/<customer_id>` に [!DNL POST] リクエストを送信します。

   ```json
   {
     "customer": {
       "email": "roni_cost@example.com",
       "firstname": "Veronica",
       "lastname": "Costello"
     }
   }
   ```

<u> 期待される結果 </u>:

顧客データが更新されます。

<u> 実際の結果 </u>:

次のエラーが発生します。

    &quot;&#39;json
    {
    &quot;message&quot;: &quot;同じメールアドレスを持つ顧客が関連付けられた web サイトに既に存在します。&quot;,
    &quot;trace&quot;: ...
    }
    &quot;&#39;

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
