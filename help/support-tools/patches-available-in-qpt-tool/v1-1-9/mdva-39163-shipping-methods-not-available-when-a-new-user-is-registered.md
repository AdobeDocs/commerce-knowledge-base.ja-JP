---
title: 「MDVA-39163：ゲストセッションの製品を使用して新しく登録したユーザーが配送方法を使用できない」
description: MDVA-39163 パッチを使用すると、新しいユーザが登録され、カート内の製品がゲスト セッションからのものである場合に発送方法が使用できない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.9 がインストールされている場合に利用できます。 パッチ ID は MDVA-39163。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: f8661a4e-5832-41bb-be3d-4ea6c863fdb9
feature: CMS, Marketing Tools, Orders, Products, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# MDVA-39163：ゲストセッションからの製品で、新しく登録されたユーザーが配送方法を使用できない

MDVA-39163 パッチを使用すると、新しいユーザが登録され、カート内の製品がゲスト セッションからのものである場合に発送方法が使用できない問題を解決できます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.9 がインストールされています。 パッチ ID は MDVA-39163。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

新しいユーザーが登録され、買い物かごの商品がゲストセッションからの場合、発送方法は使用できません。

<u>再現手順</u>:

1. に移動 **Admin** > **ストア** > **設定** > **売上** > **配信方法**. を有効にするのみ **定額料金** 発送方法と他のすべてを無効にします。
1. が含まれる **定額料金** 発送方法の「」を選択します。 **特定** で使用できる国オプション **適用可能な国に出荷** を設定し、リストから 1 つの国を選択します（例：米国）。
1. に移動 **Admin** > **ストア** > **設定** > **顧客** > **顧客設定** およびを設定 **電子メールによる確認が必要** 対象： _はい_.
1. で新しいメールテンプレートを作成 **Admin** > **Marketing** > **メールテンプレート** と読み込み `Footer (magento/luma)` テンプレートを作成し、テンプレートのコンテンツを CMS ブロックに置き換えます。

   ```CMS
   {{block class="Magento\Cms\Block\Block" block_id="footer_links_block"}}
   ```

1. に移動 **Admin** > **コンテンツ** > **デザイン** > **設定** フロントエンド web サイトに関連するテーマを選択します。 「フッターテンプレート」に、作成した新しいメールテンプレートを設定します。
1. フロントエンドに移動し、商品を買い物かごに追加します。
1. 顧客を作成すると、メールアドレスを確認するメールが届きます。 確認リンクをクリックします。 Web サイトにログインします。
1. に移動 **マイアカウント** そして、アドレスを追加します。 住所の国を、以前に管理者設定で設定した配送先国に設定します。
1. チェックアウトに移動します。

<u>期待される結果</u>:

お客様の住所が配送先国に対応しているため、配送方法が利用可能です。

<u>実際の結果</u>:

発送方法はご利用いただけません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
