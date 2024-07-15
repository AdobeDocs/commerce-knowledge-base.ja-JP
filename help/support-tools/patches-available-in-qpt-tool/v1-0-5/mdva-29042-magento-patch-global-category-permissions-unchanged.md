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

MDVA-29042 パッチでは、Commerce Admin の共有済みカタログに新しい商品が追加された後、カタログのアクセス権が自動的に「*許可*」に変更される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.5 がインストールされている場合に使用できます。 この問題は、Adobe Commerce 2.3.6 の B2B 拡張機能で修正されました。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.3.3 から 2.3.4-p2 （B2B 拡張機能を使用）

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Commerce Admin でグローバルカテゴリアクセス権からカスタマーグループの選択を解除しても、カテゴリアクセス権内でそのカスタマーグループが自動的に「*拒否*」に設定されません。

<u> 前提条件 </u>:

* 顧客グループが定義され、**STORES**/**Configuration**/**CATALOG**/**Catalog**/**Category Permissions** で選択されている B2B インスタンス：
   * **閲覧を許可カテゴリ**
   * **製品価格を表示**
   * **買い物かごへの追加を許可**
* 各 **カテゴリ** では、顧客グループは次の場合に「*許可*」と定義されます。
   * **ブラウジングカテゴリ**
   * **製品価格を表示**
   * **買い物かごに追加**

<u> 再現手順 </u>:

1. Commerce管理者で、**STORES**/**Configuration**/**CATALOG**/**Catalog**/**Category Permissions** に移動し、以下から Customer グループの選択を解除します。
   * **閲覧を許可カテゴリ**
   * **製品価格を表示**
   * **買い物かごへの追加を許可**
1. 「**設定を保存** ボタンをクリックします。
1. インデクサーが実行されるのを待ちます。
1. **カタログ**/**カテゴリ**/**カテゴリ権限** を確認します。

<u> 期待される結果 </u>:

顧客グループのすべてのカテゴリに対して、**カテゴリ権限** が&quot;*拒否*&quot;に設定されます。

<u> 実際の結果 </u>:

顧客グループのカテゴリ権限は変更されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。

B2B 会社の機能について詳しくは、開発者向けドキュメントの次の記事を参照してください。

* [B2B デベロッパーガイド ](https://devdocs.magento.com/guides/v2.4/b2b/bk-b2b.html)
* [ 会社の役割の管理 ](https://devdocs.magento.com/guides/v2.4/b2b/roles.html)
* [Adobe Commerce Enterprise B2B Extension 設定パスのリファレンス ](https://devdocs.magento.com/guides/v2.4/config-guide/prod/config-reference-b2b.html)
