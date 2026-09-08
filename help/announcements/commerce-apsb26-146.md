---
title: Adobe Commerceに関する緊急のアクションが必要なクリティカルセキュリティアップデート公開（APSB26-146）
description: Adobeは、Adobe Commerceのゼロデイ脆弱性であるCVE-2026-75650に対処するセキュリティ情報APSB26-146をリリースしました。 ホットフィックスを適用して資格情報を回転させる方法について説明します。
autotag-review: '2026-09-07T17:27:44.037Z'
TQID: 'https://experienceleague.adobe.com/ADVRRn85--ZgWtPdi4qA49fsDPVW976N4MYWp26taho'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c32adafa-ed01-4b31-997e-2413013911b0
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: e4cb6392735e3adb609d8cbd78548edff7f99570
workflow-type: tm+mt
source-wordcount: 852
ht-degree: 0%

---


# 緊急の対応が必要：Adobe Commerceに関する重要なセキュリティアップデート公開（APSB26-146）

>[!IMPORTANT]
>
>これは、CVE-2026-75650に関連する緊急のアップデートです。 Adobeは、Adobe Commerceのマーチャントをターゲットとする野生のCVE-2026-75650が悪用されていることを認識しています。

9月7日、Adobeは、Adobe CommerceとMagento Open Sourceに影響を与える重要なセキュリティアップデートをリリースしました。 Adobeは、Adobe Commerceのゼロデイ脆弱性を認識し、それを解決するためのセキュリティアップデート（APSB26-146）をリリースしました。 この脆弱性により、未認証の攻撃者が、影響を受けるインストールで任意のコードを実行する可能性があります（CVE-2026-75650）。

Adobeは、この脆弱性に対処するセキュリティ情報APSB26-146をリリースしました。 情報は次の場所で入手できます。

[Adobe Commerceに関するセキュリティアップデート公開| APSB26-146](https://helpx.adobe.com/security/products/magento/apsb26-146.html)

この記事では、Adobe CommerceおよびMagento Open Sourceの現在および以前のバージョンのホットフィックスを適用する方法について説明します。

## 説明

影響を受ける製品とバージョン：

Adobe Commerceのバージョン：

* 2.4.9-2026-aug以前
* 2.4.8-2026-aug以前
* 2.4.7-2026-aug以前
* 2.4.6-2026-aug以前
* 2.4.5-2026-aug以前
* 2.4.4-2026-aug以前

Adobe Commerce B2B版：

* 1.5.3-2026-aug以前
* 1.5.2-2026-aug以前
* 1.4.2-2026-aug以前
* 1.3.4-2026-aug以前
* 1.3.3-2026-aug以前

Magento Open Sourceのバージョン：

* 2.4.9-2026-aug以前
* 2.4.8-2026-aug以前
* 2.4.7-2026-aug以前
* 2.4.6-2026-aug以前

## 解決策

### Adobe Commerce on Cloud、Adobe Commerce オンプレミス、およびMagento Open Sourceのソリューション

影響を受ける製品とバージョンの脆弱性を解決するには、VULN-39341 パッチを（バージョンに応じて）適用し、暗号化キーをローテーションする必要があります。

互換性に関する注意：このホットフィックスは、以下に示すバージョンについてのみテストされています。 サポートされている他のバージョンでも機能する可能性がありますが、これは正式に検証されていません。

Adobe Commerceのバージョン：

* 2.4.9-2026-aug
* 2.4.8-2026-aug
* 2.4.7-2026-aug
* 2.4.6-2026-aug
* 2.4.5-2026-aug
* 2.4.4-2026-aug

Adobe Commerce B2B版：

* 1.5.3-2026-aug
* 1.5.2-2026-aug
* 1.4.2-2026-aug
* 1.3.4-2026-aug
* 1.3.3-2026-aug

Magento Open Sourceのバージョン：

* 2.4.9-2026-aug
* 2.4.8-2026-aug
* 2.4.7-2026-aug
* 2.4.6-2026-aug

### ホットフィックスリンク

影響を受ける製品バージョンに次のホットフィックスを適用します。

* [ホットフィックス VULN-39341-composer-patches.zipをダウンロードする](https://repo.magento.com/patch/VULN-39341-composer-patches.zip)

### ホットフィックスの適用方法

ファイルを解凍し、手順については、サポートナレッジベースの[Adobe](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento)が提供するコンポーザーパッチの適用方法を参照してください。

### ホットフィックスが適用されていることを確認する（Adobe Commerce Cloud版マーチャントのみ）

問題にパッチが適用されたかどうかを簡単に判断できないため、CVE-2026-75650 ホットフィックスが正常に適用されたかどうかを確認することをお勧めします。

これは、ファイル `VULN-39341_Hotfix_COMPOSER.patch`を例として使用して、次の手順を実行することによって実行できます。

1. [品質パッチ ツールをインストールします](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage#install)。
1. 次のコマンドを実行します：`vendor/bin/magento-patches -n status | grep "39341\|Status"`。
1. 次のような出力が表示されます。この例では、VULN-39341は適用済みステータスを返します。

| ID | タイトル | カテゴリ | オリジン | ステータス | Details |
|---|---|---|---|---|---|
| 該当なし | .../m2-hotfixes/VULN-39341_Hotfix_COMPOSER.patch | その他 | ローカル | 適用 | パッチタイプ：カスタム |

### パッチ適用後に資格情報を回転する

この問題を完全に解決するには、暗号化キーだけでなく、サーバー、API、統合資格情報など、暗号化または公開されているすべての資格情報をローテーションします。

>[!NOTE]
>
>暗号化キーは、統合トークン、支払いゲートウェイの資格情報、システム特権の自動化トークンの暗号化に使用されます。 暗号化キーだけを回転しても、既に公開されている可能性のある資格情報は無効になりません。 Commerce内だけでなく、ソース（支払いゲートウェイやサードパーティサービスなど）で関連するすべての資格情報をローテーションします。

資格情報をローテーションするには、次の手順に従います。

1. ホットフィックスを適用します。
1. メンテナンスモードを有効にします。
1. cron実行を無効にします（Commerce on Cloud コマンド：`vendor/bin/ece-tools cron:disable`）。
1. [暗号化キーを回転](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/encryption-key?lang=en)。
1. すべての管理者パネルユーザーパスワードを回転します。
1. すべてのREST/SOAP/GraphQL統合トークン（**[!UICONTROL System]** > **[!UICONTROL Extensions]** > **[!UICONTROL Integrations]**）を非アクティブ化して再生成します。
1. 接続されているサードパーティアプリケーションのOAuth クライアントシークレットをローテーションします。
1. プロバイダーレベルで支払いゲートウェイ APIの資格情報をローテーションします（Stripe、Braintree、Adyen、PayPalなど）。
1. データベース資格情報をローテーションします。
1. SSH/デプロイキーと、cronまたはシステム特権のサービスアカウント資格情報をローテーションします。
1. 配送、税務、その他の統合されたサードパーティ拡張機能のAPI キーを回転できます。
1. キャッシュをフラッシュします。
1. cron実行を有効にします（Commerce on Cloud コマンド：`vendor/bin/ece-tools cron:enable`）。
1. メンテナンスモードを無効にします。
1. クラウド上のCommerceのみ：新しいデータベース資格情報を適用するために再デプロイします。

### セキュリティアップデート

Adobe Commerceに関するセキュリティアップデート公開：

* [Adobeセキュリティ情報（APSB26-146）](https://helpx.adobe.com/security/products/magento/apsb26-146.html)
* [Adobe Commerceに関する最新のセキュリティアップデート](https://helpx.adobe.com/security/products/magento.html)

### 関連トピックス

Adobe Commerce インストールガイドの[&#x200B; メンテナンスモードを有効または無効にする](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode?lang=en)
