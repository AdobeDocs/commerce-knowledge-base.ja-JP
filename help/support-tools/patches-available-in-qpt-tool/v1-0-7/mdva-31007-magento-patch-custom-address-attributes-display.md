---
title: 「MDVA-31007：カスタムアドレス属性の表示」
description: MDVA-31007 パッチを使用すると、カスタムアドレス属性がマイアカウント領域の注文詳細ページとバックエンド（**Sales &gt; Orders**の場所）に正しく表示されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 43c82b66-395f-4e33-8312-9a1994862f5f
feature: Attributes, Shipping/Delivery
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# MDVA-31007: カスタム アドレス属性の表示

MDVA-31007 パッチを使用すると、カスタムアドレス属性がマイアカウント領域の注文詳細ページとバックエンド（**Sales > Orders** の場所）に正しく表示されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.7 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.0-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. 管理バックエンドにログインします。
1. **Stores**/**Attributes**/**Customer Addresses** に移動します。
1. 2 つの属性を作成します。

   * 入力タイプを設定：*ドロップダウン*。
   * 入力タイプを設定：*テキスト*。

1. **Stores**/**Configurations**/**Customer**/**Customer Configurations** に移動します。
1. *範囲* を **デフォルトストア** 表示として選択します。
1. 「**アドレステンプレート**」セクションを展開します。 上記の 2 つのカスタム属性を含めるように、*テキスト*、*テキスト 1 行* および *4}HTML} を更新します。*

   ```php
   {{depend testdropdown}}Dropdown: {{var testdropdown}}{{/depend}}    {{depend testtext}}Text: {{var testtext}}{{/depend}}
   ```

1. ストアフロントを開きます。
1. を作成し、ユーザーでログインします。
1. **マイアカウント**/**アドレス帳** に移動し、新しいアドレスを追加します（2 つのカスタム属性を入力します）。
1. 買い物かごに製品を追加し、注文します。
1. 注文成功ページで、**注文番号** リンクをクリックします。
1. 注文詳細ページで、「注文情報 **セクションを確認し** す。
1. **バックエンド**/**営業**/**注文** に移動し、上記の注文をクリックして、**住所情報** セクションを確認します。

<u> 期待される結果 </u>:

フロントエンドとバックエンドの両方で、請求先と配送先住所が期待どおりに表示されます。

<u> 実際の結果 </u>:

フロントエンドとバックエンドの両方で、請求アドレスが正しく表示されません。 ドロップダウン属性の選択したオプションが見つかりません。また、入力属性の値に属性コードが含まれています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
