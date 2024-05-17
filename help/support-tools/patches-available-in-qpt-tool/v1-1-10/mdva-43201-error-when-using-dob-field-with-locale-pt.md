---
title: 「MDVA-43201：ロケール PT で DOB フィールドを使用する際にエラーが発生する」
description: MDVA-43201 パッチは、ポルトガル語ロケールの顧客登録フォームで DOB 顧客属性を使用するとエラーが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.10 がインストールされている場合に利用できます。 パッチ ID は MDVA-43201。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 02979378-adc1-4a1a-93bf-a35ad50e6b80
feature: B2B, Cache
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# MDVA-43201：ロケール PT で DOB フィールドを使用する際にエラーが発生する

MDVA-43201 パッチは、ポルトガル語ロケールの顧客登録フォームで DOB 顧客属性を使用するとエラーが発生する問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.10 がインストールされています。 パッチ ID は MDVA-43201。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

DOB 顧客属性がポルトガル語ロケールの顧客登録フォームに追加されると、フォームにエラーが表示されます *iterator_to_array （）に渡す引数 1 は、指定された null のインターフェイス travesable を実装しなければなりません。*.

<u>前提条件</u>:

B2B モジュールがインストールされている。

<u>再現手順</u>:

1. 管理者/に移動します **ストア** > **設定** > **一般** > **ロケールオプション**、ロケールをに設定 **ポルトガル語（ポルトガル）** をクリックして、 **保存**.
1. キャッシュの再インデックスとクリア。
1. に移動 **ストア** > **属性** > **顧客**.
1. DOB 顧客属性を開いて設定 **ストアフロントに表示** 対象： **はい**.
1. からすべてを選択 **使用するフォーム**.
1. 属性を保存します。
1. フロントエンドの新しいアカウントを作成ページに移動します。

<u>期待される結果</u>:

ポルトガル語ストアの顧客登録フォームには、DOB 属性の追加に関するエラーはありません。

<u>実際の結果</u>:

ポルトガル語ストアの顧客登録フォームで、DOB 属性の追加に関してエラーが発生します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
