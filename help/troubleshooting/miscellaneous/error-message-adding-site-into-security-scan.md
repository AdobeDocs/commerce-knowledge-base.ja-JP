---
title: セキュリティスキャンにサイトを追加する際のエラーメッセージ
description: この記事では、ユーザーが[Commerce Security Scan] （https://account.magento.com/scanner/dashboard/）にサイトを追加できない場合の問題に対する可能な解決策を提供します。
exl-id: 8d000ca4-b977-432d-bb26-6ea320067a40
feature: Cache, Compliance, Console, Security
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
  - id: c4af0798-d497-5e6b-8380-19812c26d00a
    internal-label: Console
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%
---
# セキュリティスキャンにサイトを追加する際のエラーメッセージ

この記事では、ユーザーが[Commerce セキュリティスキャン &#x200B;](https://account.magento.com/scanner/dashboard/)にサイトを追加できない場合の問題に対する解決策を示します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法とバージョン）
* Magento Open Source

## イシュー

[Commerce セキュリティスキャン &#x200B;](https://account.magento.com/scanner/dashboard/)にサイトを追加できません。 サイトを追加しようとすると、次のエラーメッセージが表示されます。*スキャン用にサイトを送信できません。*

## Solution

1. 次のIP アドレスがポート 80および443でブロックされていないことを確認します。
   * 52.87.98.44
   * 34.196.167.176
   * 3.218.25.102

1. 確認コードは時間的制約があります。 **サイトを追加** リンクをクリックしてから30分以上経過した場合、コードは期限切れになっている可能性があります。
1. キャッシュをクリーンアップし、検証コードがホームページのソース本文に表示されることを忘れないでください。 確認コードは、HTML マークアップ仕様に従って挿入する必要があります。HTML コメントは、ページ本文に挿入できます（フッターセクションに配置することをお勧めします）。META タグは、ヘッドセクションにのみ挿入する必要があります。
1. **確認コードを確認**&#x200B;をクリックする前に、ブラウザーの開発者コンソールを開き、「**ネットワーク**」タブをクリックし、magento.comからの応答を確認します。 HTTP 200 （OK）で、応答本文にJSON オブジェクトを含める必要があります。
1. 応答コードがHTTP 200、応答本文がJSON オブジェクトで、`verified` プロパティ値が`false`の場合、コードがページに見つからないことを意味します。 `details` プロパティの値には、説明を含める必要があります。 例えば、ストアが自己署名SSL証明書を使用している場合、接続エラーが発生する可能性があります。

それでもサイトを追加できない場合は、次の手順を実行します。

1. ページに別のHTML コメントを配置します。

   ```HTML
   <!-- MAGEID:Your magento.com ID, EMAIL:your email address -->
   ```

1. サポートチケットを提出し、以下の情報を提供します。
   * Adobe Commerce ストア URL
   * MAGEID + Magento.comのアカウントメール
   * 名+姓
   * 会社名
   * コンマ区切り通知のメールリスト

## 関連トピックス

* ユーザーガイドの[&#x200B; セキュリティスキャン &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/security/security-scan)。
