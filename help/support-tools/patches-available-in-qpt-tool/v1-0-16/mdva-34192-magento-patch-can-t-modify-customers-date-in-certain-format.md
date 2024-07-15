---
title: 「MDVA-34192 パッチ：特定の形式の顧客の日付を変更できない」
description: MDVA-34192 パッチでは、dd/mm/yyyy 形式を使用してお客様の生年月日を変更/指定できない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.16 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 8aa36970-b2bf-43f8-ba8f-bfc144f8d4ab
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# MDVA-34192 パッチ：特定の形式で顧客の日付を変更できない

MDVA-34192 パッチでは、dd/mm/yyyy 形式を使用してお客様の生年月日を変更/指定できない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.16 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用にパッチが作成されます。** Cloud Infrastructure 2.3.5-p1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** 2.3.4～2.3.6

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

このパッチによって、いくつかの問題が解決されます。 そのうちの 1 つについて再現する説明と手順を次に示します。

カスタムの日付属性を使用してフィルターし、管理者ユーザーのロケールが en\_GB の場合、製品グリッドフィルターは正しく機能しません。

<u> 再現手順：</u>:

1. **インターフェイスロケール** が *英語（英国）* に設定されている管理者ユーザーを作成します。
1. 次の設定で日付属性を作成します。
   * **ストア所有者のカタログ入力タイプ**: *Date*
   * **フィルターオプションで使用**:*はい*
   * **列に追加オプション**:*はい*
1. 属性を属性セットに割り当てます。
1. 製品編集ページに移動し、日付選択を使用して新しい属性の日付を選択して保存します。
1. 新しい日付属性を使用して製品グリッドをフィルタリングしてみてください。

<u> 期待される結果：</u>:

管理者ユーザーのロケールが en\_GB の場合、カスタム日付属性に対する製品フィルターは正しく機能します。

<u> 実際の結果：</u>

管理者ユーザーのロケールが en\_GB の場合、カスタム日付属性の製品フィルターが正しく機能しない。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
