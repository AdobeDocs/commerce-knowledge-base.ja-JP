---
title: 「MDVA-34192 パッチ：特定の形式の顧客の日付を変更できない」
description: MDVA-34192 パッチでは、dd/mm/yyyy 形式を使用してお客様の生年月日を変更/指定できない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.16 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 8aa36970-b2bf-43f8-ba8f-bfc144f8d4ab
feature: Tools and External Services
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# MDVA-34192 パッチ：特定の形式で顧客の日付を変更できない

MDVA-34192 パッチでは、dd/mm/yyyy 形式を使用してお客様の生年月日を変更/指定できない問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.16 がインストールされています。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p1

**Adobe Commerce バージョンとの互換性：** 2.3.4-2.3.6

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

このパッチによって、いくつかの問題が解決されます。 そのうちの 1 つについて再現する説明と手順を次に示します。

カスタムの日付属性を使用してフィルターし、管理者ユーザーのロケールが en\_GB の場合、製品グリッドフィルターは正しく機能しません。

<u>再現手順：</u>:

1. 次の条件を満たす管理者ユーザーを作成 **インターフェイス ロケール** はに設定されています。 *英語（英国）*.
1. 次の設定で日付属性を作成します。
   * **店舗所有者のカタログ入力タイプ**: *日付*
   * **フィルターオプションで使用**: *はい*
   * **列に追加オプション**: *はい*
1. 属性を属性セットに割り当てます。
1. 製品編集ページに移動し、日付選択を使用して新しい属性の日付を選択して保存します。
1. 新しい日付属性を使用して製品グリッドをフィルタリングしてみてください。

<u>期待される結果：</u>:

管理者ユーザーのロケールが en\_GB の場合、カスタム日付属性に対する製品フィルターは正しく機能します。

<u>実際の結果：</u>:

管理者ユーザーのロケールが en\_GB の場合、カスタム日付属性の製品フィルターが正しく機能しない。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
