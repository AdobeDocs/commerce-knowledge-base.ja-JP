---
title: 「MDVA-29787：関連製品が表示されない」
description: MDVA-29787 パッチを使用すると、**関連製品**がAdobe Commerce ストアのフロントエンドに表示されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.6 がインストールされている場合に利用できます。 パッチ ID は MDVA-29787。
exl-id: ee060d7b-3b0e-4bd5-84e6-fbd6d2fa532f
feature: Cache, Marketing Tools, Products
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# MDVA-29787：関連製品が表示されない

MDVA-29787 パッチは、次の問題を解決します。 **関連製品** は、Adobe Commerce ストアのフロントエンドには表示されません。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.6 がインストールされています。 パッチ ID は MDVA-29787。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.3.

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.0。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

のターゲットルール **関連製品** 次の場合は機能しません：*が次の 1 つ：*&#x200B;条件「」は、 **表示する製品** Commerce Admin.

>[!NOTE]
>
>メモ：このパッチでは、既存のターゲットルールは修正されません。 既存のターゲットルールを再作成する必要があります。

<u>再現手順</u>:

1. 作成 **新しい属性** （例：Test\_Attr）。
   * を設定 **店舗所有者のカタログ入力タイプ** = *テキスト。*
   * 対象： **ストアフロント プロパティ**、設定 **プロモルール条件に使用** = *はい*.
1. 作成 **新規属性セット** （例：Test\_Set）。
1. を追加 **新しい属性** に **新規属性セット** （例：「Test\_Set」属性セットに「Test\_Attr」属性を追加）。
1. 3 つの製品を作成します。 例えば、次のように設定されます。
   * Product1, Test\_Attr = MAGT2NA\_Test3
   * Product2, Test\_Attr = 24-MB02
   * Product3, Test\_Attr = 701644329389M
1. ターゲットを作成 **ルール** （**Marketing**   > **関連する製品ルール** をクリックし、 **ルールを追加** ボタン）。 設定：
   * **適用先** = *関連製品*
   * **一致する製品**
   * 作成した新しい属性を設定 **。対象：** **上記の手順 1** を Product1 の属性にします（例：Test\_Attr = MAGT2NA\_Test3）。
   * **表示する製品** =他の 2 つの製品の属性（例：24-MB02 および 701644329389M 属性）
1. を保存します **ルール**.
1. 必要に応じて、再インデックスを実行します。
1. キャッシュをクリアします。
1. フロントエンドで Product1 を開きます。

<u>期待される結果</u>:

関連製品が存在する。

<u>実際の結果</u>:

関連製品がありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
