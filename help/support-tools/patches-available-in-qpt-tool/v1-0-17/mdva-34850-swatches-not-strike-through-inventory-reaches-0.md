---
title: 「MDVA-34850：スウォッチのストライクスルーされないインベントリが「0」に達する」
description: MDVA-34850 パッチでは、在庫が「0」に達してもスウォッチが開かず、他の在庫内スウォッチへの製品詳細ページ（PDP）リンクに表示されない問題が修正されています。 また、管理者設定では**在庫切れ製品を表示**も*はい*に設定されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.17 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 90f5cef4-137a-426d-a447-2d1aca23e6c1
feature: Inventory, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# MDVA-34850：スウォッチの取り消し在庫が「0」に達する

MDVA-34850 パッチでは、在庫が「0」に達してもスウォッチが開かず、他の在庫内スウォッチへの製品詳細ページ（PDP）リンクに表示されない問題が修正されています。 この **在庫切れ商品を表示** も次のように設定 *はい* 管理設定で。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.17 がインストールされています。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.1 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

デフォルトの在庫在庫が使用中でない場合、在庫切れの製品オプションが PDP ページに表示されない **在庫切れ商品を表示** 設定が有効になっています。

<u>前提条件</u>:

* マルチソースインベントリ（MSI）のインストール
* での在庫切れ製品の表示を有効にする [在庫在庫オプション](https://docs.magento.com/user-guide/configuration/catalog/inventory.html).

<u>再現手順</u>:

1. 新しい在庫在庫\[New Stock\] を作成し、すべての Web サイトをその在庫と上記のソースに割り当てます。 これで、デフォルトの在庫は使用されなくなります。
1. を作成 [設定可能な製品](https://docs.magento.com/user-guide/catalog/product-create-configurable.html) 3 つのサイズ オプション \[S,M,L\] を追加します。
1. 各オプションを開き、作成したカスタム ソース \[new\_source\] のみを割り当てて数量を追加します。 また、\[Source Status\] を\[In Stock\] に設定します。
1. 再インデックスを実行し、フロントエンドから設定可能な製品を確認します。 3 つのオプションがすべて表示されます。
1. バックエンドから\[size:S\] に割り当てられたシンプルな商品を開き、\[Source Status\] を\[Out of Stock\] に設定し、数量も 0 に更新します。 再インデックスを実行し、フロントエンドから設定可能な製品を確認します。

<u>期待される結果</u>:

在庫切れ商品を表示オプションが有効になっているので、3 つのオプションがすべて表示されます。 在庫切れオプション \[S\] は無効にして削除する必要があります。 フロントエンドとバックエンドの注文の詳細には、価格= 12x2 の 2 倍の 1 つのオプション製品が表示されます。

<u>実際の結果</u>:

在庫切れオプションは非表示です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
