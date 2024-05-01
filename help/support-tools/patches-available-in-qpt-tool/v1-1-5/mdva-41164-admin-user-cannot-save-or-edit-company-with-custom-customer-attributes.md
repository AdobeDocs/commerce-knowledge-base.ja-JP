---
title: 「MDVA-41164：カスタム顧客属性を持つ会社を保存または編集できない」
description: MDVA-41164 パッチを使用すると、管理者ユーザーが、ファイルまたは画像のカスタム顧客属性を持つ会社を保存または編集できない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-41164。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 24338895-68b4-404c-bedd-46cfc7e983a0
feature: Admin Workspace, Attributes, B2B, Companies
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# MDVA-41164: カスタム顧客属性を持つ会社を保存または編集できない

MDVA-41164 パッチを使用すると、管理者ユーザーが、ファイルまたは画像のカスタム顧客属性を持つ会社を保存または編集できない問題を解決できます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.5 がインストールされています。 パッチ ID は MDVA-41164。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーが、どのタイプのファイルまたは画像のカスタム顧客属性を持つ会社を保存または編集できません。

<u>前提条件</u>:

B2B モジュールがインストールされています。

<u>再現手順</u>:

1. で会社を有効にする **ストア** > **設定** > **B2B の機能**.
1. での顧客属性の作成 **ストア** > **属性** > **顧客** > **新しい属性を追加**:
   * 入力タイプ : ファイル（添付）
   * ストアフロントに表示：はい
   * 並べ替え順：任意
   * で使用するForms：すべてを選択
1. に会社を新規作成します。 **顧客** > **会社** > **新しい会社を追加** そして、上記で作成した新しい属性用のファイルをアップロードします。

<u>期待される結果</u>:

ユーザーが会社の作成を完了でき、添付ファイルがエラーなくアップロードされる。

<u>実際の結果</u>:

* 次のエラーメッセージが表示されます。 *ファイルの保存中にエラーが発生しました。*
* 例外ログには、次のようなレコードが含まれます。

  ```php
  report.CRITICAL: Notice: Undefined index: customer in
  ../app/code/Magento/Customer/Controller/Adminhtml/File/Customer/Upload.php on line 69
  ```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
