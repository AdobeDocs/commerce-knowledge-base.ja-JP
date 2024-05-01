---
title: サイトをセキュリティ スキャンに追加するときに表示されるエラーメッセージ
description: この記事では、ユーザーが [Commerce Security Scan] （https://account.magento.com/scanner/dashboard/）にサイトを追加できない場合に発生する可能性のある問題の解決策を説明します。
exl-id: 8d000ca4-b977-432d-bb26-6ea320067a40
feature: Cache, Compliance, Console, Security
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# サイトをセキュリティ スキャンに追加するときに表示されるエラーメッセージ

この記事では、ユーザーがにサイトを追加できない問題の解決策について説明します [Commerce セキュリティスキャン](https://account.magento.com/scanner/dashboard/).

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法とバージョン）
* Magento Open Source

## 問題

ユーザーがにサイトを追加できない [Commerce セキュリティスキャン](https://account.magento.com/scanner/dashboard/). サイトを追加しようとすると、次のエラーメッセージが表示されます。 *スキャン用のサイトを送信できません。*

## 解決策

1. 次の IP アドレスがポート 80 と 443 でブロックされていないことを確認します。
   * 52.87.98.44
   * 34.196.167.176
   * 3.218.25.102

1. 確認コードは時間に依存します。 次の期間が 30 分以上経過した場合 **サイトを追加** リンクがクリックされました。コードの有効期限が切れている可能性があります。
1. キャッシュをクリーンアップし、検証コードがホームページのソース本文に表示されることを忘れないでください。 確認コードは、HTMLマークアップの仕様に従って挿入する必要があります。HTMLコメントは、ページ本文に挿入できます（フッターセクションに挿入することをお勧めします）。META タグは、head セクションにのみ挿入する必要があります。
1. クリック前 **確認コードの確認**&#x200B;を開き、ブラウザーの開発者コンソールで、 **ネットワーク** tab キーを押して、magento.comからの応答を確認します。 HTTP 200 （OK）である必要があり、応答本文には JSON オブジェクトが含まれている必要があります。
1. 応答コードが HTTP 200 で、応答本文が JSON オブジェクトである場合、および `verified` プロパティの値： `false`ページにコードが見つからないことを意味します。 この `details` プロパティ値には、説明を含める必要があります。 例えば、ストアで自己署名 SSL 証明書を使用している場合、接続エラーが発生する可能性があります。

それでもサイトを追加できない場合は、次の手順を実行します。

1. ページに別のHTMLコメントを配置します。

   ```HTML
   <!-- MAGEID:Your magento.com ID, EMAIL:your email address -->
   ```

1. サポートチケットを送信し、次の情報を提供します。
   * Adobe Commerce ストアの URL
   * MAGEID + Magento.com アカウントのメール
   * 名+姓
   * 会社名
   * 通知メールのコンマ区切りリスト

## 関連資料

* [セキュリティスキャン](https://docs.magento.com/user-guide/magento/security-scan.html) を参照してください。
