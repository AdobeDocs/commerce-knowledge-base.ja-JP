---
title: 「ACSD-46815：静的コンテンツのデプロイがコンパクト戦略を使用して失敗する」
description: ACSD-46815 パッチを適用すると、コンパクト戦略を使用した際に静的コンテンツのデプロイが失敗するAdobe Commerceの問題を修正できます。
exl-id: e94a0911-5cd9-4866-a027-7ea3239555d3
feature: Deploy, Page Content, SCD
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# ACSD-46815：コンパクト戦略を使用すると静的コンテンツのデプロイに失敗する

ACSD-46815 パッチは、コンパクトな方法を使用した場合に静的コンテンツのデプロイメントが失敗する問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](https://support.magento.com/hc/en-us/articles/360047139492) 1.1.20 がインストールされています。 パッチ ID は ACSD-46815 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

コンパクトな戦略でデプロイすると、静的コンテンツのデプロイメントが失敗します。

<u>再現手順</u>:

1. 次のコマンドを実行して、静的コンテンツをコンパクトな方法でデプロイします。

```bash
bin/magento setup:static-content:deploy -f -s compact
```

<u>期待される結果</u>:

静的コンテンツのデプロイメントはエラーなしで完了します。

<u>実際の結果</u>:

静的コンテンツのデプロイメントが失敗し、コンパクトな戦略が返される。 デプロイメントプロセス中に次のエラーが発生します。 */app/pub/static/adminhtml/folder/base/default/のMagentoのコンテンツ。/node_modules/@spectrum-css/vars/dist/spectrum-global.css ファイルを読み取れません。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
