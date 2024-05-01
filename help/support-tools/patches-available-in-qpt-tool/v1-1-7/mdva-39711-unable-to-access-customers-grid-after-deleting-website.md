---
title: 「MDVA-39711:web サイトを削除した後、顧客グリッドにアクセスできない」
description: MDVA-39711 パッチを適用すると、管理者ユーザーが Web サイトを削除した後に顧客のグリッドにアクセスできない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.7 がインストールされている場合に利用できます。 パッチ ID は MDVA-39711。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 46bef304-9360-4b69-b064-631725de381c
feature: Configuration
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# MDVA-39711:Web サイトを削除した後、顧客グリッドにアクセスできない

MDVA-39711 パッチを適用すると、管理者ユーザーが Web サイトを削除した後に顧客のグリッドにアクセスできない問題が修正されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.7 がインストールされています。 パッチ ID は MDVA-39711。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7-p2、2.3.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーが、web サイトを削除した後、顧客のグリッドにアクセスできません。

<u>再現手順</u>:

1. 新しい web サイト、ストア、ストア表示を作成します。
1. 管理者で新しい顧客を作成し、作成した web サイトに関連付けます。
1. に移動 **ストア** > **すべてのストア** 作成した web サイトを削除します。
1. に移動 **顧客** > **すべての顧客**.

<u>期待される結果</u>:

* エラーメッセージは表示されない。
* すべての顧客がグリッドに表示されます。

<u>実際の結果</u>:

* ユーザーに次のエラーメッセージが表示されます。 *要求された ID 2 の Web サイトが見つかりませんでした。 Web サイトを確認して、もう一度試してください*
* すべての顧客が表示されるわけではありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
