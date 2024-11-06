---
title: 「MDVA-33606：階層に割り当てられたCMS ページを保存するとエラーが発生する」
description: MDVA-33606 パッチは、階層ツリーに割り当てられたCMS ページを保存すると、「Unique constraint violation found」というエラーが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.3 がインストールされている場合に利用できます。 パッチ ID は MDVA-33606。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: cdefece5-6d13-4003-87e9-810c665e940c
feature: CMS
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# MDVA-33606：階層に割り当てられたCMS ページを保存するとエラーが発生する

MDVA-33606 パッチを使用すると、階層ツリーに割り当てられたCMS ページを保存する際に *Unique constraint violation found* エラーが発生する問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.3 がインストールされている場合に使用できます。 パッチ ID は MDVA-33606。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1-2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

階層ツリーに割り当てられたCMS ページを保存しようとすると、「*一意の制約違反が見つかりました*」というエラーメッセージが表示されます。

<u> 再現手順 </u>:

1. 新しいCMSページを作成します。 範囲をすべてのストア表示に設定します。 これはCMSの Page 1 です。
1. 新しいストア表示を作成します。 これはストア表示 2 です。
1. **コンテンツ**/**階層**/CMS Page 1 を階層ツリーに追加に移動します。
1. 範囲を Store View 2 に変更します。
   * 「親ノード階層を使用」のチェックを外します。
   * この範囲にCMS Page 1 を追加し、保存します。
1. 次に、範囲をデフォルトのストア表示に変更します。
   * 「親ノード階層を使用」のチェックを外します。
   * この範囲にCMS Page 1 を追加し、保存します。
1. **コンテンツ**/**ページ**/**新しいページを追加** に移動します。
   * ページに Page 2 というタイトルを付けます。
   * 「Web サイトのページ」セクションで、すべてのストア表示と両方のストア表示（デフォルトのストア表示とストア表示 2）に割り当て、「**ページを保存**」をクリックします。
1. CMSの編集ページで、「階層」タブを開きます。
   * 「Page 2」を「Store View 2」ノード、「Default」ノード、「All Websites」ノードに割り当てます。

<u> 期待される結果 </u>:

エラーを起こすことなく、CMSページを 3 つのノードすべてに割り当てることができます。

<u> 実際の結果 </u>:

次のエラーが表示されます：*一意の制約違反が見つかりました*。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
