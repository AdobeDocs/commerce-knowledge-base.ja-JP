---
title: 「MDVA-29148:ArrayBackend が保存時にデフォルト値を割り当てない」
description: MDVA-29148 パッチは、「\Magento\Eav\Model\Entity\Attribute\Backend\ArrayBackend」が保存時にデフォルト値を割り当てない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 7b2f5c18-0e7a-485b-a07e-700e435697fd
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# MDVA-29148: ArrayBackend は保存時に既定値を割り当てません

MDVA-29148 パッチは、保存時にデフォルト値が割り当てら `\Magento\Eav\Model\Entity\Attribute\Backend\ArrayBackend` ない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.7 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.3-p1。

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） >=2.3.0 &lt;2.4.2.

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

インポートスクリプトまたは REST API を使用して製品を作成する場合、`\Magento\Eav\Model\Entity\Attribute\Backend\ArrayBackend` バックエンドモデルを使用し、デフォルト値を持つ属性は、デフォルト値が割り当てられません。

<u> 再現手順 </u>:

1. `\Magento\Eav\Model\Entity\Attribute\Backend\ArrayBackend` バックエンドモデルと空でないデフォルト値を使用する、新しいグローバル属性を作成します。
1. REST API を使用して、新しい製品を作成します。
1. その新しい製品を REST API から取得し、製品のカスタム属性に属性が存在しないことを確認します。

<u> 期待される結果 </u>:

カスタム属性のデフォルト値が製品属性に保存されました。

<u> 実際の結果 </u>:

カスタム属性の既定値が製品属性に保存されませんでした。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
