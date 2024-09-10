---
title: 「ACSD-58446:GraphQLで子ユーザーまたはチームを持つチームを削除すると、情報が不明なエラーメッセージが表示される」
description: ACSD-58446 パッチを適用すると、GraphQLを介して子ユーザーまたはチームを持つチームを削除すると、UI に一致しない非情報エラーメッセージが返されるAdobe Commerceの問題が修正されます。
feature: GraphQL
role: Admin, Developer
source-git-commit: d64689d83943691883fc853af22631288d4999a8
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# ACSD-58446:GraphQLを使用してチームを子ユーザーまたはチームと削除すると、未情報のエラーメッセージが表示される

ACSD-58446 パッチは、GraphQLを介して子ユーザーまたはチームを持つチームを削除すると、UI と一致しない非情報エラーメッセージが返されるAdobe Commerceの問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.49 がインストールされている場合に使用できます。 パッチ ID は ACSD-58446 です。 この問題はAdobe Commerce B2B 1.5.1 で修正される予定です

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p7

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQLを使用してチームを子ユーザーまたはチームと削除すると、UI に一貫性のない非情報エラーメッセージが返される。

## 前提条件：

Adobe Commerce B2B モジュールがインストールされている。

<u> 再現手順 </u>:

1. *[!UICONTROL Company]* 機能を有効にします。
1. 新しい会社アカウントを作成します。
1. **[!UICONTROL Admin]** にログインし、会社アカウントをアクティブにします。
1. メールを確認し、新しい会社アカウントのパスワードを設定します。
1. 会社の新しいチームを作成します。
1. ストアフロントに会社ユーザーとしてログインし、作成したチームに新しいユーザーを追加します。
1. **[!UICONTROL Admin]** にログインし、会社ユーザーを無効にして、*[!UICONTROL Customer Active]* = *いいえ* を設定します
1. 作成したチームは必ずGraphQLから削除してください。

   ```
   mutation {
     deleteCompanyTeam(
       id: "MQ=="
     ) {
       success
     }
   }
   ```

<u> 期待される結果 </u>:

UI と一致する情報エラーメッセージが返されます。

<u> 実際の結果 </u>:

UI と一致しない、一般的な内部サーバーエラーメッセージが返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
