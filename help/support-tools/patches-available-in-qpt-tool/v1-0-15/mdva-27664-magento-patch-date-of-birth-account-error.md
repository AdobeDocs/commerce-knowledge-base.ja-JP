---
title: 「MDVA-27664 パッチ：生年月日アカウントエラー」
description: MDVA-27664 パッチを使用すると、お客様のアカウントの生年月日が現在よりも大きくなる可能性がある問題を解決できます。
exl-id: c669764e-b4a5-4031-92ac-1156755e9a0a
feature: Customer Service
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# MDVA-27664 パッチ：生年月日アカウント エラー

MDVA-27664 パッチを使用すると、お客様のアカウントの生年月日が現在よりも大きくなる可能性がある問題を解決できます。

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.15 がインストールされています。 この問題は、Adobe Commerce バージョン 2.3.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.4 - 2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. 管理者にログインします。
1. を設定 **Locale** = *en\_GB* （英国）ユーザーの場合。
1. 顧客を編集します。
1. 今年の月の 12 日より後の生年月日を選択してください。

<u>期待される結果</u>:

生年月日が有効なので、顧客情報は期待どおりに保存できます。

<u>実際の結果</u>:

検証エラーが発生したため、顧客情報を保存できません：

```php
The Date of Birth should not be greater than today.
```

ここで、日付は DD/MM/YYYY 日付形式ではなく、MM/DD/YYYY 日付形式として扱われます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
