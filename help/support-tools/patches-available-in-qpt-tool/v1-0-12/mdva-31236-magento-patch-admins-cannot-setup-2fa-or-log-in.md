---
title: 「MDVA-31236：管理者が 2FA を設定したり、ログインしたりできない」
description: MDVA-31236 パッチは、カスタムリソースアクセス権を持つCommerce管理者ユーザーが [two-factor authentication （2FA） ] （https://docs.magento.com/user-guide/stores/security-two-factor-authentication.html）をセットアップしたり、ログインしたりできない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.12 がインストールされている場合に利用できます。
exl-id: b75d7a19-3c17-4389-b359-7aeeb8797539
feature: Admin Workspace
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# MDVA-31236：管理者が 2FA を設定したり、ログインしたりできない

MDVA-31236 パッチでは、カスタムリソースアクセス権を持つCommerce管理者ユーザーが設定できない問題が修正されています [2 要素認証（2FA）](https://docs.magento.com/user-guide/stores/security-two-factor-authentication.html) またはログインします。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.12 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.0-2.4.1.

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者権限を持たないユーザーは、現在、個人用の 2FA アクセスを設定できません。 Adobe Commerceに実装されている 2FA には、2 つの ACL ロールが含まれます。 1 つの役割は、グローバルシステム設定に影響を及ぼし、システムの設定時にのみ必要になります。 2 つ目の ACL の役割は、個々のユーザー 2FA アカウントに影響します。 管理者ユーザーは、この 2 番目のタイプの 2FA ACL を設定する必要があります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
