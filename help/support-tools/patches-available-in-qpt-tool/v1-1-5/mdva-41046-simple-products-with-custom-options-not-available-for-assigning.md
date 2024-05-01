---
title: 「MDVA-41046：割り当てにカスタムオプションを使用できないシンプルな製品」
description: MDVA-41046 パッチは、カスタム オプションを持つシンプルな製品を設定可能/グループ化された製品に割り当てることができない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-41046。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 01229a69-c72a-4189-9be5-1761073b74ee
feature: Products
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# MDVA-41046：割り当てにカスタムオプションを使用できないシンプルな製品

MDVA-41046 パッチは、カスタム オプションを持つシンプルな製品を設定可能/グループ化された製品に割り当てることができない問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.5 がインストールされています。 パッチ ID は MDVA-41046。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カスタムオプションを使用したシンプルな製品は、設定可能/グループ化された製品に割り当てることはできません。

<u>再現手順</u>:

1. カスタマイズ可能なオプションを含むシンプルな製品を作成し、configurable 属性の値を設定します。
   * 使用方法 *カラー* 設定可能な属性として、を選択します。 *黄* カラー値として使用します。
1. シンプルな製品を保存します。
1. 次に、設定可能な製品を作成ページに移動します。
1. 「設定を作成」ウィザードを実行し、次の項目を選択します *黄* 属性の色として使用します。
1. 設定可能な製品を保存せずに、「選択」ドロップダウンから「別の製品を選択」オプションを選択します。
1. これにより、色属性イエローでフィルタリングされた製品グリッドが開きます。 次に、カスタマイズ可能なオプションを使用して以前に作成したシンプルな製品を選択します。
1. 設定可能な商品を保存します。

<u>期待される結果</u>:

カスタムオプションを含むシンプルな製品は、手順 6 の割り当て（グリッドに表示）に使用できます。

<u>実際の結果</u>:

構成セクションが空です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
