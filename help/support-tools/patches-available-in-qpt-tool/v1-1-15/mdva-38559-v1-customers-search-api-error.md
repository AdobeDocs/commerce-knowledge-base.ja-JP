---
title: 'MDVA-38559: /V1/customers/search API returns error'
description: MDVA-38559 パッチは、複数のサブスクリプションを持つお客様に対して「/V1/customers/search」 API がエラーを返す問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.15 がインストールされている場合に利用できます。 パッチ ID は MDVA-38559。 この問題はAdobe Commerce 2.4.3 で修正されていることに注意してください。
exl-id: 434fe78c-c384-4fa8-b26a-cb00007e490e
feature: REST, Search
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# MDVA-38559: /V1/customers/search API はエラーを返します

MDVA-38559 パッチにより、 `/V1/customers/search` 複数のサブスクリプションを持つ顧客に対して API がエラーを返す。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.15 がインストールされています。 パッチ ID は MDVA-38559。 この問題はAdobe Commerce 2.4.3 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`/V1/customers/search` 複数のサブスクリプションを持つ顧客に対して API がエラーを返す。

<u>前提条件</u>:

Adobe Commerce ストアは複数の web サイトを使用しています。

<u>再現手順</u>:

1. に移動 **ストア** > **設定** > **顧客** > **顧客設定** > **アカウント共有オプション** を選択して、 **グローバル**.
1. に移動 **顧客** > **すべての顧客**&#x200B;を選択 **編集** 任意の顧客で、次のいずれかを選択します **ニュースレター**.
1. 複数の web サイトのニュースレターを購読して、顧客を保存します。
1. 次のリクエストを送信します。

```REST API
V1/customers/search?searchCriteria[filterGroups][0][filters][0][field]=email&searchCriteria[filterGroups][0][filters][0][value]=test@example.com&searchCriteria[filterGroups][0][filters][0][conditionType]=eq
```

<u>期待される結果</u>:

顧客の検索結果が表示されます。

<u>実際の結果</u>:

次のエラーが exception.log に記録されます。 *同じ ID &#39;&#39;1&#39;&#39;の項目（Magento\Customer\Model\Customer\Interceptor）が既に存在します。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
