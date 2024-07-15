---
title: 「ACSD-48857：で編集した後に変更を保存できません  [!DNL Page Builder]」
description: ' [!DNL Page Builder] を使用して編集した後、ユーザーが変更を保存できないAdobe Commerceの問題を修正するために、ACSD-48857 パッチを適用します。'
exl-id: c95b354d-8954-4e9c-9e92-8a64f62f0a68
feature: Admin Workspace, CMS, Page Builder
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# ACSD-48857: [!DNL Page Builder] で編集した後に変更を保存できない

ACSD-48857 パッチは、[!DNL Page Builder] で編集した後、ユーザーが変更を保存できない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされている場合に使用できます。 パッチ ID は ACSD-48857 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL Page Builder] で編集した後、ユーザーが変更を保存できない。

<u> 再現手順 </u>

1. 管理者 Web サイトにログインします。
1. **[!UICONTROL Content]**/**[!UICONTROL Elements]**/**[!UICONTROL Pages]** に移動して、空の CMS ページを作成します。
1. この SQL スクリプトを実行して、次の **[!UICONTROL Content]** フィールド値を設定します。

   ```SQL
   update cms_page set content = '<div data-content-type="text" data-appearance="default" data-element="main"><h4 style="text-align: center;" contenteditable="true" data-placeholder="Edit Heading Text" data-content-type="heading" data-appearance="default" data-element="main">THE RULES</h4></div>' where page_id=8;
   ```

1. 管理者で **[!UICONTROL Content]**/**[!UICONTROL Elements]**/**[!UICONTROL Pages]** に戻ります。
1. ページを編集します。
1. 「**[!UICONTROL Content]**」タブに移動します。
1. 「**[!UICONTROL Save]**」をクリックします。

<u> 期待される結果 </u>

HTMLコンテンツのサニタイズが実装されます。 これにより [!DNL Page Builder] テキストエディターで生成されたコンテンツ内の予約されたHTML属性が削除されます。

<u> 実績 </u>

ページは保存されず、ローダーは回転を続けます。 コンソールで、次のエラーが生成されます。

```
[ERROR] Page Builder was rendering for 5 seconds without releasing locks.
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
