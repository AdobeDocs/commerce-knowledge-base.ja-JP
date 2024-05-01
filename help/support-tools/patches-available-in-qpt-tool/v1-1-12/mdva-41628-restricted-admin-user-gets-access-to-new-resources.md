---
title: 「MDVA-41628：制限付き管理者ユーザーが新しいリソースにアクセスする」
description: MDVA-41628 パッチは、新しいモジュールが追加されたときに、制限された管理者ユーザーが新しいリソースにアクセスできる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-41628。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 8f63ce9d-07b6-4d9d-a51b-b85b783b2adf
feature: Admin Workspace
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# MDVA-41628：制限付き管理者ユーザーは、新しいリソースにアクセスできます

MDVA-41628 パッチは、新しいモジュールが追加されたときに、制限された管理者ユーザーが新しいリソースにアクセスできる問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-41628。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

制限付き管理者ユーザーは、新しいモジュールが追加されると、新しいリソースにアクセスできます。

<u>再現手順</u>:

1. リソースが制限された管理者ユーザーロールを新規作成します。
1. 手順 1 で作成した役割の下に、新しい管理者ユーザーを作成します。
1. 新しいメニュー項目のセットと ACL リソースを作成するカスタムモジュールをインストールして有効にします。
1. 新しく作成した管理者ユーザーを使用してログインします。

<u>期待される結果</u>:

アクセスが制限された管理者ユーザーは、新しく作成されたメニュー項目にアクセスできません。

<u>実際の結果</u>:

制限付き管理者ユーザーは、新しいリソースがユーザーロールに割り当てられていない場合でも、新しいメニュー項目にアクセスできます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
