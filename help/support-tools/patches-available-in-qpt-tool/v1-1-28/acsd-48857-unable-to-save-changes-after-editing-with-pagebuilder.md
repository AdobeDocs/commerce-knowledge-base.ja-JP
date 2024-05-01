---
title: 'ACSD-48857：で編集した後に変更を保存できない [!DNL Page Builder]'
description: を使用して編集した後、ユーザーが変更を保存できないAdobe Commerceの問題を修正するために ACSD-48857 パッチを適用してください [!DNL Page Builder].
exl-id: c95b354d-8954-4e9c-9e92-8a64f62f0a68
feature: Admin Workspace, CMS, Page Builder
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# ACSD-48857：でを編集した後に変更を保存できない [!DNL Page Builder]

ACSD-48857 パッチは、で編集した後、ユーザーが変更を保存できない問題を修正します [!DNL Page Builder]. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされています。 パッチ ID は ACSD-48857 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

で編集した後、ユーザーが変更を保存できない [!DNL Page Builder].

<u>再現手順</u>

1. 管理者 Web サイトにログインします。
1. に移動します。 **[!UICONTROL Content]** > **[!UICONTROL Elements]** > **[!UICONTROL Pages]** 空の CMS ページを作成します。
1. この SQL スクリプトを実行して、次の内容を設定します **[!UICONTROL Content]** フィールド値：

   ```SQL
   update cms_page set content = '<div data-content-type="text" data-appearance="default" data-element="main"><h4 style="text-align: center;" contenteditable="true" data-placeholder="Edit Heading Text" data-content-type="heading" data-appearance="default" data-element="main">THE RULES</h4></div>' where page_id=8;
   ```

1. に戻る **[!UICONTROL Content]** > **[!UICONTROL Elements]** > **[!UICONTROL Pages]** 管理画面
1. ページを編集します。
1. に移動します **[!UICONTROL Content]** タブ。
1. クリック **[!UICONTROL Save]**.

<u>期待される結果</u>

HTMLコンテンツのサニタイズが実装されます。 これにより、が削除されます [!DNL Page Builder] テキストエディターで生成されたコンテンツ内の予約済みHTML属性。

<u>実際の結果</u>

ページは保存されず、ローダーは回転を続けます。 コンソールで、次のエラーが生成されます。

```
[ERROR] Page Builder was rendering for 5 seconds without releasing locks.
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
