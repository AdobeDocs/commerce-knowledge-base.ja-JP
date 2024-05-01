---
title: 「ACSD-48058：バンドルされた製品が web サイトに割り当てられていない場合、製品価格の再インデックスが機能しない」
description: バンドルされた製品がいずれの Web サイトにも割り当てられていない場合に製品の価格の再インデックスが機能しないAdobe Commerceの問題を修正するには、ACSD-48058 パッチを適用してください。
exl-id: 691371f1-7f10-4be6-80e4-821e7cf664a6
feature: Admin Workspace, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# ACSD-48058：バンドルされた製品が web サイトに割り当てられていない場合、製品価格のインデックス再作成が機能しない

ACSD-48058 パッチは、バンドルされた製品が Web サイトに割り当てられていない場合、製品の価格インデックス再作成が機能しない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされています。 パッチ ID は ACSD-48058 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） >=2.4.5 &lt; 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

バンドルされた製品が Web サイトに割り当てられていない場合、製品価格の再インデックスが機能しません。

<u>再現手順</u>:

1. Adobe Commerce管理者に移動します **[!UICONTROL Catalog]** > **[!UICONTROL Products]** 新しいバンドル製品を作成するか、既存のバンドル製品を編集します。
   * 「」をクリック **[!UICONTROL Product in Websites]** tab キーを押して、すべてのチェックボックス（web サイト）のチェックボックスをオフにします
   * 商品の保存
1. 再インデックスを実行します。

<u>期待される結果</u>:

再インデックスが正常に実行されました。

<u>実際の結果</u>:

製品価格インデックスの実行中に次のエラーがスローされます。

```bash
Undefined array key <bundel product id > in vendor/magento/module-bundle/Model/ResourceModel/Indexer/Price/DisabledProductOptionPriceModifier.php on line 117
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
