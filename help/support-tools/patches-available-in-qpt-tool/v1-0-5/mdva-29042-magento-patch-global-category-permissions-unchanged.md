---
title: 「MDVA-29042：グローバルカテゴリ権限が変更されない」
description: MDVA-29042 パッチでは、Commerce Admin の共有済みカタログに新しい商品が追加された後、カタログのアクセス権が自動的に「*許可*」に変更される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.5 がインストールされている場合に利用できます。 この問題は、Adobe Commerce 2.3.6 の B2B 拡張機能で修正されました。
exl-id: 491b8881-87ec-4820-8f87-54961682e961
feature: Catalog Management, Categories, Customer Service, Roles/Permissions
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# MDVA-29042: グローバル カテゴリのアクセス許可は変更されません

MDVA-29042 パッチは、カタログのアクセス許可が&quot; &quot;に変更された問題を修正します&#x200B;*許可* Commerce管理者の共有カタログに新しい商品が追加されると、が自動的に「。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.5 がインストールされています。 この問題は、Adobe Commerce 2.3.6 の B2B 拡張機能で修正されました。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.3.3 から 2.3.4-p2 （B2B 拡張機能を使用）

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Commerce Admin でグローバルカテゴリ権限からカスタマーグループの選択を解除しても、そのカスタマーグループは自動的には「」に設定されません&#x200B;*拒否*&#x200B;カテゴリ権限内。

<u>前提条件</u>:

* 顧客グループが定義され以下で選択されている B2B インスタンス **ストア** > **設定** > **カタログ** > **カタログ** > **カテゴリ権限** 対象：
   * **閲覧を許可カテゴリ**
   * **製品価格を表示**
   * **カートへの追加を許可**
* 各の下 **カテゴリ**&#x200B;顧客グループは「」と定義されます&#x200B;*許可*」に移動します。
   * **ブラウジングカテゴリ**
   * **製品価格を表示**
   * **カートに追加**

<u>再現手順</u>:

1. Commerce Admin で、に移動します。 **ストア** > **設定** > **カタログ** > **カタログ** > **カテゴリ権限** およびから顧客グループの選択を解除します。
   * **閲覧を許可カテゴリ**
   * **製品価格を表示**
   * **カートへの追加を許可**
1. 「」をクリックします **設定を保存** ボタン。
1. インデクサーが実行されるのを待ちます。
1. を見る **カタログ** > **カテゴリ** > **カテゴリ権限**.

<u>期待される結果</u>:

**カテゴリ権限** はに設定されます。*拒否*」と表示されます（顧客グループのすべてのカテゴリの場合）。

<u>実際の結果</u>:

顧客グループのカテゴリ権限は変更されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。

B2B 会社の機能について詳しくは、開発者向けドキュメントの次の記事を参照してください。

* [B2B デベロッパーガイド](https://devdocs.magento.com/guides/v2.4/b2b/bk-b2b.html)
* [会社の役割の管理](https://devdocs.magento.com/guides/v2.4/b2b/roles.html)
* [Adobe Commerce Enterprise B2B Extension 設定パスのリファレンス](https://devdocs.magento.com/guides/v2.4/config-guide/prod/config-reference-b2b.html)
