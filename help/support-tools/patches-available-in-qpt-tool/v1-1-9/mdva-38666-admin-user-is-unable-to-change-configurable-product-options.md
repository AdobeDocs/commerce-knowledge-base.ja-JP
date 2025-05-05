---
title: 「MDVA-38666：管理者ユーザーが、設定可能な製品オプションを変更できない」
description: MDVA-38666 パッチは、管理者ユーザーが顧客の買い物かごで設定可能な製品オプションを変更できない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.9 がインストールされている場合に利用できます。 パッチ ID は MDVA-38666。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 72440e47-1deb-41da-a225-d4bc73029ad5
feature: Admin Workspace, Configuration, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# MDVA-38666：管理者ユーザーが、設定可能な製品オプションを変更できない

MDVA-38666 パッチは、管理者ユーザーが顧客の買い物かごで設定可能な製品オプションを変更できない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.9 がインストールされている場合に使用できます。 パッチ ID は MDVA-38666。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーは、顧客の買い物かごで設定可能な製品オプションを変更できません。

<u> 再現手順 </u>:

1. 顧客アカウント範囲をグローバルに設定します。
1. ストアを含む 2 つの web サイトを作成します。
1. 設定可能な 2 つの製品を作成して、各 web サイトに割り当てます。
1. フロントエンドで顧客アカウントを作成し、ログインします。
1. 買い物かごに製品を追加してチェックアウトを行います（これは、各 web サイトで見積もり ID を異ならせるために行われます）。
1. 商品を買い物かごに追加して、そのままにします。
1. 2 つ目の web サイトに切り替えて、製品を買い物かごに追加します（顧客アカウントの範囲がグローバルに設定されているので、同じログインが機能します）。
1. 管理者から顧客を開き、「買い物かご」タブに移動します。
1. ドロップダウンからストアを切り替え、設定を変更してみてください。

<u> 期待される結果 </u>:

設定可能なオプションを含むポップアップが表示されます。

<u> 実際の結果 </u>:

ポップアップフォームは表示されません。 ユーザーは設定を変更できません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
