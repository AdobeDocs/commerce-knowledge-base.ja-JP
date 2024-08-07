---
title: 「MDVA-29954：間違ったアドレスが新しい会社ユーザー登録メールを送信しました」
description: MDVA-29954 パッチを使用すると、「新しい会社の登録リクエスト」と「会社へのリンクが完了しました」というメールが、誤ったメールアドレスから送信される問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.8 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 9b3d1b93-3fe6-40a0-a68a-3e3d789c6d66
feature: B2B, Communications, Companies
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# MDVA-29954：間違ったアドレスが新しい会社ユーザー登録メールを送信しました

MDVA-29954 パッチを使用すると、「新しい会社の登録リクエスト」と「会社へのリンクが完了しました」というメールが、誤ったメールアドレスから送信される問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.8 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.5-p2、2.4.0、2.4.1。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 前提条件 </u>:

**B2B 機能を備え、** 会社 **が有効になっている B2B** Adobe Commerceをインストールします。

<u> 再現手順 </u>:

1. ストアフロントの **アカウントを作成** ドロップダウンをクリックし、**新しい会社アカウントを作成** を選択します。
1. 必須フィールドに入力し、アカウントを登録します。
1. バックエンド（**顧客**/**会社**）から **会社** を有効にします。
1. 登録に使用したメールアドレスを確認します。
1. メールで送信された手順に従って、**会社管理者パスワード** を設定します。
1. **会社管理者パスワード** を使用して、フロントエンドにログインします。
1. **マイアカウント**/**会社ユーザー**/**新しいユーザーの追加** に新しい **会社ユーザー** を作成します。
1. **ストア**/**設定**/**一般ストアのメールアドレス**/**一般連絡先** に移動し、「**送信者のメール**」にチェックを入れます。
1. 手順 7 で **新規ユーザー** の登録に使用したメールに移動します。

<u> 期待される結果 </u>:

「あなたが会社にリンクされている」メールは、手順 8 の **送信者メール** と同じ値を持つメールアドレスから送信されます。

<u> 実際の結果 </u>:

「あなたは会社にリンクされています」というメールが **会社管理者** メールから送信されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
