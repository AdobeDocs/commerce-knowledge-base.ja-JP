---
title: 「ACSD-43887：チェックアウト支払いページに間違った詳細が表示される」
description: ACSD-43887 パッチは、会社の発注書が有効になっている場合に、チェックアウトの支払いページに誤った詳細が表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.17 がインストールされている場合に利用できます。 パッチ ID は ACSD-43887 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 07b17f96-5236-43a7-aeaf-6bfe36c551cf
feature: B2B, Checkout, Orders, Payments, User Account
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# ACSD-43887：チェックアウト支払いページに間違った詳細が表示される

ACSD-43887 パッチは、会社の発注書が有効になっている場合に、チェックアウトの支払いページに誤った詳細が表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.17 がインストールされている場合に使用できます。 パッチ ID は ACSD-43887 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

会社の発注書が有効になっている場合、チェックアウトの支払いページに正しくない詳細が表示される。

<u> 前提条件 </u>:

1. B2B モジュールがインストールされている。
1. 「会社を有効化」が「はい _に設定されている_。 **ストア**/**設定**/**一般**/**B2B 機能**/**会社を有効化**/**はい** に移動します。
1. 「発注の有効化」が _Yes_ に設定されている。 **Order Approval Configuration**/**Enable Purchase Orders**/**Yes** に移動します。
1. PayPal Express は、支払い方法として設定されます。

<u> 再現手順 </u>:

1. 仮想製品を作成します。
1. 会社の管理者とフロントエンドから会社アカウントを登録します。
1. バックエンドから会社アカウントを承認し、会社の承認時に **発注書を有効にする** を _はい_ に設定します。
1. フロントエンドに移動し、手順 2 で作成した会社の管理者アカウントを使用してログインします。
1. 会社の「デフォルトユーザー」を作成します。 **会社ユーザー**/**新規ユーザーを追加** に移動します。
1. 会社の「承認ルール」を作成します。 **承認ルール**/**新しいルールを追加** に移動します。

   * ルールタイプ：注文合計
   * 注文の合計：$1 以上
   * 次のユーザーの承認が必要：会社管理者

1. 「デフォルトユーザー」アカウントを使用してログアウトしてログインします。
1. 手順 1 で作成した仮想製品を買い物かごに追加し、チェックアウトに進みます。
1. 支払い方法として PayPal Express を選択し、**注文書を作成** をクリックします。
1. 会社の管理者アカウントを使用してログアウトしてログインします。
1. **自分の発注書** に移動し、**会社の発注書** から **表示** をクリックして、手順 9 で作成した注文を表示します。
1. 発注書を承認します。 発注書のステータスは、「承認済：支払保留中」にする必要があります。
1. 会社の「デフォルトユーザー」アカウントを使用してログアウトしてログインします。
1. **自分の発注書**/**表示**/**注文を行う** に移動します。
1. **注文概要** を確認します。

<u> 期待される結果 </u>:

注文概要に、正しいゼロ以外の値が表示されます。

<u> 実際の結果 </u>:

注文の概要の合計値はゼロです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
