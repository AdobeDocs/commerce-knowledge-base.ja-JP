---
title: 「MDVA-38799：ダウンロード可能な製品がステージング更新の作成後に保存されない」
description: MDVA-38799 パッチを使用すると、ステージング アップデートの作成後にダウンロード可能な製品が保存されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.0 がインストールされている場合に利用できます。 パッチ ID は MDVA-38799。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: 306f9ef3-ca3a-41b9-a5d3-42aa4ef59953
feature: Products, Staging
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# MDVA-38799：ステージング更新プログラムの作成後にダウンロード可能な製品が保存されない

MDVA-38799 パッチを使用すると、ステージング アップデートの作成後にダウンロード可能な製品が保存されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.0 がインストールされている場合に使用できます。 パッチ ID は MDVA-38799。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0-2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ダウンロード可能な製品は、ステージングアップデートの作成後は保存されません。 次のエラーメッセージが表示されます。*ダウンロード可能なサンプルは製品に関連していません。 リンクを確認して、もう一度やり直してください*。

<u> 再現手順 </u>:

1. **カタログ**/**製品** に移動します。
1. 「製品を追加」の横のドロップダウンをクリックし、「ダウンロード可能な製品」を選択します。
   * 商品の名前、SKU、価格、数量を入力します。
1. ダウンロード可能な情報ページまでスクロールします。
1. 「サンプル」で、「**リンクを追加**」をクリックします。
   * タイトル、ファイルをアップロードを入力します（ファイルのタイプは関係ありません）。
1. **保存** をクリックします。 次のメッセージが表示されます。*製品を保存しました*。
1. ページ上部の「**新規更新をスケジュール**」をクリックします。
   * 更新名、および有効な開始日と終了日を入力します。
1. ステージングの更新で「**保存**」をクリックします。
1. 製品の **保存** をクリックします。

<u> 期待される結果 </u>:

製品はエラーなしで保存されます。

<u> 実際の結果 </u>:

次のエラーメッセージが表示されます。*ダウンロード可能なサンプルは製品に関連していません。 リンクを確認して、もう一度やり直してください*。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
