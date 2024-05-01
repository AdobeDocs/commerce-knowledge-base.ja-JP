---
title: Adobe Commerce管理者の URL の場所が公開されました
description: この記事では、管理パネルの URL の場所を公開できる、Adobe Commerceのセキュリティ問題に対するパッチを提供します。 URL の場所を把握することで、攻撃の自動化が容易になる場合があります。
exl-id: fe147ad5-6019-46c1-b48c-6b957b6e1582
feature: Admin Workspace
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Adobe Commerce管理者の URL の場所が公開されました

この記事では、管理パネルの URL の場所を公開できる、Adobe Commerceのセキュリティ問題に対するパッチを提供します。 URL の場所を把握することで、攻撃の自動化が容易になる場合があります。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.X.X 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.X.X
* Magento Open Source 2.X.X

## 問題

Magento Open SourceとAdobe Commerceで問題が見つかりました。この問題を使用して、管理パネルの URL の場所を開示することができます。 現在のところ、この問題が直接侵害につながると信じる理由はありませんが、URL の場所を知ることで攻撃の自動化が容易になる可能性があります。

## 解決策

この問題を修正するには、この記事に添付されているパッチを適用してください。 ダウンロードするには、次のリンクをクリックします。

* Download [PRODSECBUG-2432\_EE\_2.1.17\_composer.patch](assets/PRODSECBUG-2432_EE_2.1.17_composer.patch.zip) - バージョン 2.1.13～2.1.17、Adobe Commerce、Magento Open Sourceの場合
* Download [PRODSECBUG-2432\_EE\_2.2.8\_composer.patch](assets/PRODSECBUG-2432_EE_2.2.8_composer.patch.zip) - バージョン 2.2.0～2.2.8 の場合、すべてのエディション
* Download [PRODSECBUG-2432\_EE\_2.3.1\_composer.patch](assets/PRODSECBUG-2432_EE_2.3.1_composer.patch.zip) - バージョン 2.3.0～2.3.1 の場合、すべてのエディション

製品またはバージョンのパッチが表示されない場合は、最新のセキュリティリリースにアップグレードしてからパッチを適用してください。

Adobeは、発作の症状がまったくない場合でも、できるだけ早くパッチを適用することを強くお勧めします。

## パッチの適用方法

参照： [Adobe Commerceが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 説明を参照してください。

## その他のセキュリティ推奨事項

また、Adobeでは、マーチャントがツールをデプロイして、二要素認証、VPN、IP許可リストに加えるなどの管理パネルを保護することを強くお勧めします。 詳しくは、次のブログとドキュメントを参照してください。

* [ブルートフォースの攻撃に対するProtectへの 5 つの即時対応](https://magento.com/security/best-practices/5-immediate-actions-protect-against-brute-force-attacks)
* [新しい更新を推測するMagento インストール パスワードをProtectしてください](https://magento.com/security/best-practices/protect-your-magento-installation-password-guessing-new-update)
* [セキュリティのベストプラクティス](https://magento.com/security/best-practices/security-best-practices)
* Adobe Commerceでの二要素認証の追加と設定 [2.3.x](https://docs.magento.com/user-guide/v2.3/stores/security-two-factor-authentication.html) および [2.4.x](https://docs.magento.com/user-guide/stores/security-two-factor-authentication.html)
