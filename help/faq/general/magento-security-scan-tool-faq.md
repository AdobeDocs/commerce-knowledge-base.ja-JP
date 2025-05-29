---
title: Adobe Commerce セキュリティスキャンツールに関するよくある質問
description: この記事では、Adobe Commerce セキュリティスキャンツールに関するよくある質問（FAQ）に回答します。
exl-id: 380ce617-e3d9-491b-b425-8489abd3c541
feature: Compliance
source-git-commit: cff17a83648e10e85d95a5895acd8d1916a8eef9
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Adobe Commerce セキュリティスキャンツールに関するよくある質問

この記事では、Adobe Commerce セキュリティスキャンツールに関するよくある質問（FAQ）に回答します。

## セキュリティスキャンツールとは何ですか？また、誰のために書かれていますか？ {#what-is-the-magento-security-scan-tool-and-who-is-it-written-for}

セキュリティスキャンツールは、当社のマーチャント、開発者、および担当者が責任を持って指定した担当者が利用できる無料のツールで、セキュリティリスクについてサイトを監視できます。 商店のマルウェアをプロアクティブかつ効率的に検出し、セキュリティ上のリスク、マルウェア、脅威がある場合は商店に通知できます。

## セキュリティスキャンツールは、すべてのAdobe Commerce マーチャントが使用できますか？ {#is-magento-security-scan-tool-available-to-all-magento-merchants}

はい。セキュリティスキャンツールは、すべてのAdobe CommerceおよびMagento Open Sourceのマーチャントが使用できます。

## セキュリティ スキャン ツールを使用してサイトをスキャンできるユーザーはいますか？ {#can-anyone-scan-my-site-with-the-magento-security-scan-tool}

いいえ。マーチャントがトークンでスキャンをリクエストする際に、サイトをAdobe Commerce アカウントに結び付けます。 これはサイトごとに一意です。

## Web ストア上のAdobe Commerce以外のページをスキャンできますか？ {#can-the-tool-scan-non-magento-pages-on-my-webstore}

セキュリティスキャンツールは、Adobe Commerce ドメインの脆弱性をスキャンするように設計されています。 セキュリティスキャンツールを使用してAdobe Commerce以外のページの脆弱性をスキャンすると、信頼性の低い結果になる可能性があります。 Adobe Commerce以外の他のプラットフォームで生成されたページをセキュリティスキャンツールを使用してスキャンしないことを強くお勧めします。

## スキャン ツールから特定のセキュリティ テストを除外できますか？ {#can-i-exclude-specific-security-tests-from-magento-scan-tool}

Security Scan Tool のマーチャントは、Adobe Commerceの Security Scan Tool スキャンから特定のセキュリティ テストを除外することはできません。 セキュリティ スキャン ツールの各セキュリティ テストは、セキュリティ リスク、マルウェア、および脅威を特定する際にマーチャントを支援するために作成されます。

## いくらですか？ {#what-does-it-cost}

セキュリティスキャンツールは無料です。 マーチャントは、セキュリティスキャンの結果またはサイトの設定に基づいてAdobe Commerceの法的責任の免除を受け入れる必要があります。

## セキュリティスキャンツールの仕組み {#how-does-the-magento-security-scan-tool-work}

セキュリティスキャンツールは Web ベースで、マーチャントのオンラインAdobe Commerceアカウント（[account.magento.com](https://account.magento.com/)）からアクセスします。 セキュリティスキャンは、HTTP と HTTPS の両方で動作します。 セキュリティに関する既知の問題がないかどうかを確認し、Adobe Commerceのパッチやアップデートが見つからないかどうかを特定します。

## セキュリティ スキャン ツールを使用するには、サインアップ方法を教えてください。 {#how-do-i-sign-up-to-use-the-magento-security-scan-tool}

マーチャントは、セキュリティスキャンツールを使用してAdobe Commerce アカウント（[account.magento.com](https://account.magento.com)）から web ストアをスキャンするように登録できます。 リンクに従って、セキュリティ スキャン ツール [ ここ ](https://account.magento.com/scanner/dashboard/?_ga=2.83981338.267715797.1615821601-2099431409.1611073686) にサインアップします。

## スキャンレポートで偽陽性が表示された場合はどうすればよいですか？ {#what-do-i-do-if-i-come-across-a-false-positive-in-the-scan-report}

すべてのスキャンに失敗したことを調査し、問題を解決するために適切な措置を講じることをマーチャントにお勧めします。 調査後、マーチャントが偽陽性と思われるスキャン結果に遭遇した場合、マーチャントに対し、Adobeに適切な措置を講じるよう通知するようリクエストします。

偽陽性レポートを送信するには、Adobe Commerce マーチャントサポートにチケットを入れます。これにより、偽陽性の評価、必要な変更、および今後そのような通知が表示されないようにするための推奨事項の提供が可能になります。
