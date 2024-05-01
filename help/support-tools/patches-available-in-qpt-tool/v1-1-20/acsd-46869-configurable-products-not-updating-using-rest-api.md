---
title: 「ACSD-46869：設定可能な製品がチェックアウト時に REST API を使用して更新されない」
description: ACSD-46869 パッチを適用すると、チェックアウト時に設定可能な製品が REST API を使用して更新されない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.20 がインストールされている場合に利用できます。 パッチ ID は ACSD-46869 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: d1bac489-f0f3-4b50-bc48-86c844230da7
feature: REST, Checkout, Configuration, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# ACSD-46869：設定可能な製品が、チェックアウト時に REST API を使用して更新されない

ACSD-46869 パッチにより、チェックアウト時に設定可能な製品が REST API を使用して更新されない問題が修正されました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.20 がインストールされています。 パッチ ID は ACSD-46869 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL QPT] ランディングページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な製品は、チェックアウト時に REST API を使用して更新されません。

<u>再現手順</u>:

1. カラー属性とサイズ属性を使用して設定可能な商品を作成します。
1. を選択 **[!UICONTROL Options]** 商品を買い物かごに追加します。
1. に移動 **[!UICONTROL Checkout]**、数量を除きサイズを複数回更新し、リクエストと応答を確認します。
1. サイズを更新すると、次の応答が表示されます。

```REST API
{"extension_attributes":{"configurable_item_options":[
{"option_id":"960","option_value":25083},
{"option_id":"801","option_value":177}
]}}
```

<u>期待される結果</u>:

値は変更に従って更新されます。

<u>実際の結果</u>:

`option_value` が更新されないので、注文されると、古いサイズ値が使用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tools] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) 『品質向上パッチツール』マニュアルの「」を参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/check-patch-for-magento-issue-with-magento-quality-patches.html) サポートナレッジベースで。

で利用可能なその他のパッチについて [!DNL QPT]を参照してください。 [で使用可能なパッチ [!DNL QPT]](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) 『品質向上パッチツール』マニュアルの「」を参照してください。
