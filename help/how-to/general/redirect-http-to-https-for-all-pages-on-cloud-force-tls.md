---
title: クラウドインフラストラクチャー上のAdobe Commerceのすべてのページに対する HTTP の HTTPS へのリダイレクト（TLS を強制）
description: Commerce管理者で Fastly の**Force TLS**機能を有効化して、クラウドインフラストラクチャストア上のAdobe Commerceのすべてのページに対してグローバル HTTP から HTTPS へのリダイレクトを有効にします。
exl-id: 71667f52-a99a-47a6-99d8-10532364870f
feature: Cache, Cloud
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceのすべてのページに対する HTTP の HTTPS へのリダイレクト（TLS を強制）

Commerce管理者で Fastly の **Force TLS** 機能を有効化して、クラウドインフラストラクチャストア上のAdobe Commerceのすべてのページに対してグローバル HTTP から HTTPS へのリダイレクトを有効にします。

この記事では、詳細な [ 手順 ](#steps)、強制 TLS 機能の概要、影響を受けるバージョン、関連ドキュメントへのリンクを示します。

## 手順 {#steps}

### 手順 1：セキュア URL を設定 {#step-1-configure-secure-urls}

この手順では、ストアのセキュア URL を定義します。 既に完了している場合は、[ 手順 2:Force TLS の有効化 ](#step-2-enable-force-tls) に進みます。

1. Commerce Admin にログインします。
1. **ストア**/**設定**/**一般**/**Web** に移動します。
1. 「**ベース URL （セキュア）**」セクションを展開します。    ![magento-admin_base-urls-secure.png](assets/magento-admin_base-urls-secure.png)
1. **セキュアベース URL** フィールドに、ストアの HTTPS URL を指定します。
1. **ストアフロントでセキュアな URL を使用** 設定および **管理者でセキュアな URL を使用** 設定を **はい** に設定します。    ![magento-admin_base-urls-secure-settings.png](assets/magento-admin_base-urls-secure-settings.png)
1. 右上隅の **設定を保存** をクリックして、変更を適用します。

**ユーザーガイドの関連ドキュメント：**   [URL を保存 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/site-store/store-urls).

### 手順 2:Force TLS を有効にする {#step-2-enable-force-tls}

1. Commerce管理者で、**ストア**/**設定**/**詳細**/**システム** に移動します。
1. 「**フルページキャッシュ**」セクション、「**Fastly 設定**」、「**詳細設定**」の順に展開します。
1. **TLS を強制** ボタンをクリックします。    ![magento-admin_force-tls-button.png](assets/magento-admin_force-tls-button.png)
1. 表示されるダイアログで、「**アップロード**」をクリックします。    ![magento-admin_force-tls-confirmation-dialog.png](assets/magento-admin_force-tls-confirmation-dialog.png)
1. ダイアログが閉じた後、「TLS を強制」の現在の状態が **有効** と表示されていることを確認します。    ![magento-admin_force-tls-enabled.png](assets/magento-admin_force-tls-enabled.png)

**関連する Fastly ドキュメント：**   Adobe Commerce 2 の [Force TLS ガイド ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md)。

## Force TLS について

TLS （Transport Layer Security）は、セキュリティの低い先行プロトコルである SSL （Secure Socket Layer）プロトコルに代わる、セキュリティで保護された HTTP 接続のためのプロトコルです。

Fastly の TLS 強制機能を使用すると、サイトページに対するすべての暗号化されていない受信要求を TLS に強制できます。

&#x200B;>>
これは、暗号化されていないリクエストに対して *301 Moved Permanently* 応答を返すことで機能し、TLS と同等の値にリダイレクトされます。 例えば、*http://www.example.com/foo.jpeg&rbrace; に対してリクエストを行* と、*https://www.example.com/foo.jpeg* にリダイレクトされます。

[ 通信の確保 ](https://docs.fastly.com/guides/securing-communications/) （Fastly 関連ドキュメント）

## 影響を受けるバージョン

* **クラウドインフラストラクチャー上のAdobe Commerce:**
   * バージョン：2.1.4 以降
   * プラン：クラウドインフラストラクチャー上のAdobe Commerce スタータープランアーキテクチャとクラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャ（Pro Legacy を含む）
* **Fastly:** 1.2.4

## routes.yaml での変更は必要ありません

ストアの **すべて** のページで HTTP から HTTPS へのリダイレクトを有効にするために、ページを `routes.yaml` 設定ファイルに追加する必要はありません。ストア全体で「TLS をグローバルに強制」を有効にする（Commerce管理者を使用）だけで十分です。

## 関連する Fastly ドキュメント

* [Adobe Commerce 2 用 Force TLS ガイド ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md)
* [TLS リダイレクトの強制 ](https://docs.fastly.com/guides/securing-communications/forcing-a-tls-redirect)
* [ 意思疎通の確保 ](https://docs.fastly.com/guides/securing-communications/)
