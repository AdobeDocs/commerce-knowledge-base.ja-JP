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

MDVA-31236 パッチでは、カスタムリソースアクセス権を持つCommerce管理者ユーザーが [2 要素認証（2FA） ](https://docs.magento.com/user-guide/stores/security-two-factor-authentication.html) を設定したり、ログインしたりできない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.12 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

**このパッチは、Adobe Commerce バージョン用に作成されます。** Adobe Commerce on cloud infrastructure 2.4.0

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.0～2.4.1。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者権限を持たないユーザーは、現在、個人用の 2FA アクセスを設定できません。 Adobe Commerceに実装されている 2FA には、2 つの ACL ロールが含まれます。 1 つの役割は、グローバルシステム設定に影響を及ぼし、システムの設定時にのみ必要になります。 2 つ目の ACL の役割は、個々のユーザー 2FA アカウントに影響します。 管理者ユーザーは、この 2 番目のタイプの 2FA ACL を設定する必要があります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
