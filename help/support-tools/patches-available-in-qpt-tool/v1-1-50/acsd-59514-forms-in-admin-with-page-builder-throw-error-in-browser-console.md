---
title: 「ACSD-59514：ブラウザーコンソールの管理者のFormsで  [!DNL Page Builder]  スローエラーが発生する」
description: ACSD-59514 パッチを適用すると、管理者のフォームで「[!DNL Page Builder] はロックを解除せずに 5 秒間レンダリングしてい  [!DNL Page Builder]  した」というエラーがスローされるAdobe Commerceの問題が修正されます。 フォームの送信後にブラウザーコンソールで開き、変更を保存できない。
feature: Page Builder
role: Admin, Developer
source-git-commit: 19ecaa6b287d63bfae00c51911b53e1ed7ab5ed8
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---


# ACSD-59514：ブラウザーコンソールの投 [!DNL Page Builder] エラーを伴う管理画面のForms

ACSD-59514 パッチは、[!DNL Page Builder] を持つ管理画面のフォームが、ロックを解除せずにレンダリングしてい *[!DNL Page Builder]エラーを 5 秒間スローする問題を修正しました。フォームの送信後にブラウザーコンソールを* リックすると、変更を保存できない。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.50 がインストールされている場合に使用できます。 パッチ ID は ACSD-59514 です。 この問題はAdobe Commerce 2.4.8 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p8

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p7

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL Page Builder] を使用している管理者のFormsで、レンダリング中のエラー *[!DNL Page Builder]ロックを解放せずに 5 秒間スローされる。フォームの送信後にブラウザーコンソールを* リックすると、変更を保存できない。

<u> 前提条件 </u>:

Adobe Commerce [!DNL Page Builder] モジュールがインストールされ、有効になっています。

<u> 再現手順 </u>:

1. 管理パネルを開き、「[!UICONTROL Content]」ボタンをクリックします。
1. ブロックを選択し、ブロックを編集します。
1. コンテンツを変更し、「変 [!UICONTROL Save]」をクリックします。
1. コンソールを開き、エラーメッセージを確認します。

<u> 期待される結果 </u>:

ブロックが正常に保存されました。

<u> 実際の結果 </u>:

ローダーは回転を停止せず、ブロックは保存されません。 次のエラーがブラウザーコンソールに表示されます。
*[!DNL Page Builder]は、ロックを解除せずに 5 秒間レンダリングされていました。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
