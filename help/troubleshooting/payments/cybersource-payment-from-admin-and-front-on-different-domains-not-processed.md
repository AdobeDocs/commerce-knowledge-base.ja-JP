---
title: 異なるドメインで管理者およびフロントからサイバーソースに対する支払いが処理されません
description: この記事では、異なるドメイン上にある場合に、ストアフロントとAdobe Commerce管理者の両方からサイバーソースの支払いを処理できないことに関連する、Commerce 2.3.0 の既知の制限に対するパッチを提供します。
exl-id: 948d5907-70bd-4890-bc8a-23e04b116018
feature: Admin Workspace, Orders, Payments
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 異なるドメインで管理者およびフロントからサイバーソースに対する支払いが処理されません

この記事では、異なるドメイン上にある場合に、ストアフロントとAdobe Commerce管理者の両方からサイバーソースの支払いを処理できないことに関連する、Commerce 2.3.0 の既知の制限に対するパッチを提供します。

>[!NOTE]
>
>コアとなるAdobe Commerce Cybersource の支払い統合は 2.3.3 以降で非推奨となり、2.4.0 で完全に削除される予定です。の使用 [公式の延長](https://marketplace.magento.com/cybersource-global-payment-management.html) 代わりに、marketplace から。

## 問題

Cybersource 統合の以前の実装では、1 つのドメインからのみ支払いを処理することができました。 その結果、Adobe Commerce ストアフロントがCommerce管理者とは異なるドメインにある場合、管理者で Cybersource を使用して注文しようとすると次のエラーが発生します。」 *X-Frame-Options によって読み込みが拒否されました：https://%your\_domain%/cybersource/SilentOrder/TokenResponse/はクロスオリジンフレーミングを許可しません。* ...」

<u>再現手順</u>:

1. 別のサブドメインで管理者を設定します。
1. の下のストアにサイバーソースを設定します。 **ストア** > 設定 > **設定** > **売上** > **支払い方法** > **CyberSource**.
1. に移動 **売上** > **注文件数**.
1. 新しい注文を作成します。
1. 顧客を新規作成します。
1. 顧客詳細を入力します。
1. 注文の詳細（製品、発送方法）を入力します。
1. 支払方法として「Cybersource」を選択します。
1. 注文を送信します。

<u>期待される結果</u>：問題なく注文されます。

<u>実際の結果</u>：注文ページには読み込み中のアイコンが表示されますが、注文は行われません。 エラーはコンソールに表示されます。

## 解決策

添付のパッチは、Cybersource との統合の改善を提供します。 パッチを適用した後、管理者で支払いを処理するために Cybersource でもう 1 つのプロファイルを作成し、Commerce管理者の Cybersource 設定に必要な資格情報を追加する必要があります **ストア** > 設定 > **設定** > **売上** > **支払い方法** > **CyberSource**.

>[!NOTE]
>
>この機能強化は、Adobe Commerce オンプレミスおよびクラウドインフラストラクチャ 2.2.9 と 2.3.1 に含まれています。

## パッチ

この記事には、複数のパッチ（バージョンごとに異なるパッチ）が添付されています。 パッチをダウンロードするには、記事の最後までスクロールしてファイル名をクリックするか、次のリンクをクリックします。

* [MDVA-5914\_EE\_2.1.9\_COMPOSER\_v3.patch のダウンロード](assets/MDVA-5914_EE_2.1.9_COMPOSER_v3.patch.zip)
* [MDVA-8609\_EE\_2.2.2\_COMPOSER\_v2.patch のダウンロード](assets/MDVA-8609_EE_2.2.2_COMPOSER_v2.patch.zip)
* [MDVA-12964\_EE\_2.2.5\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-12964_EE_2.2.5_COMPOSER_v1.patch.zip)
* [MDVA-16643\_EE\_2.3.0\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-16643_EE_2.3.0_COMPOSER_v1.patch.zip)

## 互換性のあるAdobe Commerce バージョン

パッチは、パッチ ファイル名に示されている特定のバージョンに対して作成されました。 例えば、MDVA-5914\_EE\_2.1.9\_COMPOSER\_v3.patch はAdobe Commerce 2.1.9 用に作成されたもので、このバージョンで使用するのに最適なパッチです。

パッチは、次のバージョンとも互換性があります。

* Adobe Commerce オンプレミス 2.1.3～2.1.17、Adobe Commerce on cloud infrastructure 2.1.5～2.12 （MDVA-5914\_EE\_2.1.9\_COMPOSER\_v3.patch）
* Adobe Commerce オンプレミス 2.2.0～2.2.3、Adobe Commerce on cloud infrastructure 2.2.0～2.2.3 （MDVA-8609\_EE\_2.2.2\_COMPOSER\_v2.patch）
* Adobe Commerce オンプレミス 2.2.4～2.2.7、Adobe Commerce on cloud infrastructure 2.2.4～2.2.7 （MDVA-12964\_EE\_2.2.5\_COMPOSER\_v1.patch）
* Adobe Commerce オンプレミス 2.2.8、2.3.0、Adobe Commerce on cloud infrastructure 2.3.0 （MDVA-16643\_EE\_2.3.0\_COMPOSER\_v1.patch）

## パッチの適用方法

手順については、を参照してください [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。

## 添付ファイル
