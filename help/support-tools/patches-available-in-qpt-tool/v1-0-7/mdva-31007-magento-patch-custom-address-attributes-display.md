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

MDVA-31007 パッチを使用すると、カスタムアドレス属性がマイアカウント領域の注文詳細ページとバックエンド（ **「売上」 > 「受注」** 場所）。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.0-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. 管理バックエンドにログインします。
1. に移動します。 **ストア** > **属性** > **顧客アドレス**.
1. 2 つの属性を作成します。

   * 入力タイプを設定： *ドロップダウン*.
   * 入力タイプを設定： *テキスト*.

1. に移動します。 **ストア** > **設定** > **顧客** > **顧客設定**.
1. を選択 *範囲* as **デフォルトストア** 表示。
1. を展開します。 **アドレステンプレート** セクション。 更新 *テキスト*, *1 行のテキスト*、および *HTML* 上記の 2 つのカスタム属性を含めるには：

   ```php
   {{depend testdropdown}}Dropdown: {{var testdropdown}}{{/depend}}    {{depend testtext}}Text: {{var testtext}}{{/depend}}
   ```

1. ストアフロントを開きます。
1. を作成し、ユーザーでログインします。
1. に移動 **マイアカウント** > **アドレス帳**&#x200B;新しいアドレスを追加します（2 つのカスタム属性を入力します）。
1. 買い物かごに製品を追加し、注文します。
1. 注文成功ページで、 **オーダー番号** リンク。
1. 注文の詳細ページで、を確認します **オーダー情報** セクション。
1. に移動 **バックエンド** > **売上** > **注文件数**&#x200B;をクリックし、上記の順序を確認します。 **住所の情報** セクション。

<u>期待される結果</u>:

フロントエンドとバックエンドの両方で、請求先と配送先住所が期待どおりに表示されます。

<u>実際の結果</u>:

フロントエンドとバックエンドの両方で、請求アドレスが正しく表示されません。 ドロップダウン属性の選択したオプションが見つかりません。また、入力属性の値に属性コードが含まれています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
