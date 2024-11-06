---
title: 「MDVA-39966:en_US 以外のロケールをデプロイできません」
description: MDVA-39966 パッチは、ユーザーが en_US 以外のロケールをデプロイできない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-39966。 この問題は、Adobe Commerce バージョン 2.4.1 で修正されました。
exl-id: fc0f5ef4-f6be-4f0d-af8d-803b411510a9
feature: Deploy
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# MDVA-39966: en_US 以外のロケールをデプロイできません

MDVA-39966 パッチは、ユーザーが en_US 以外のロケールをデプロイできない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.2 がインストールされている場合に使用できます。 パッチ ID は MDVA-39966。 この問題は、Adobe Commerce バージョン 2.4.1 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.5-p2、2.4.0 ～ 2.4.0-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

en_US 以外のロケールをデプロイできません。

<u> 再現手順 </u>:

1. 異なるロケール（例：en_US と de_DE）で 2 つのストア表示を設定します。
1. 次のコマンドを実行して、これらのロケールの静的コンテンツをデプロイしてみてください。

```bash
bin/magento setup:static-content:deploy --language=en_US
bin/magento setup:static-content:deploy --language=de_DE
```

<u> 期待される結果 </u>:

de_DE ロケールがデプロイされます。

```bash
bin/magento setup:static-content:deploy --language=de_DE

Deploy using quick strategy
adminhtml/Magento/backend/de_DE         2416/2416           ============================ 100%   9 secs
frontend/Magento/blank/de_DE            2486/2486           ============================ 100%   7 secs
frontend/Magento/luma/de_DE             2504/2504           ============================ 100%   8 secs

Execution time: 27.062166929245
```

<u> 実際の結果 </u>:

de_DE の代わりにデプロイされた en_US ロケール：

```bash
bin/magento setup:static-content:deploy --language=de_DE

Deploy using quick strategy
adminhtml/Magento/backend/en_US         2416/2416           ============================ 100%   2 secs
frontend/Magento/blank/en_US            2486/2486           ============================ 100%   1 sec
frontend/Magento/luma/en_US             2504/2504           ============================ 100%   2 secs
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
