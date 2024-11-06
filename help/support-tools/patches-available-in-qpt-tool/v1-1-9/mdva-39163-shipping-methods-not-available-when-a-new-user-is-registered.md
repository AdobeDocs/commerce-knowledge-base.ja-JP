---
title: 「MDVA-39163：ゲストセッションの製品を使用して新しく登録したユーザーが配送方法を使用できない」
description: MDVA-39163 パッチを使用すると、新しいユーザが登録され、カート内の製品がゲスト セッションからのものである場合に発送方法が使用できない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.9 がインストールされている場合に利用できます。 パッチ ID は MDVA-39163。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: f8661a4e-5832-41bb-be3d-4ea6c863fdb9
feature: CMS, Marketing Tools, Orders, Products, Shipping/Delivery
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# MDVA-39163：ゲストセッションからの製品で、新しく登録されたユーザーが配送方法を使用できない

MDVA-39163 パッチを使用すると、新しいユーザが登録され、カート内の製品がゲスト セッションからのものである場合に発送方法が使用できない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.9 がインストールされている場合に使用できます。 パッチ ID は MDVA-39163。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

新しいユーザーが登録され、買い物かごの商品がゲストセッションからの場合、発送方法は使用できません。

<u> 再現手順 </u>:

1. **管理者**/**ストア**/**設定**/**営業**/**配信方法** に移動します。 **定額** の配送方法のみを有効にし、それ以外はすべて無効にします。
1. **定額** 配送方法で、「**該当する国に発送**」設定で使用可能な **特定** 国オプションを選択し、リストから 1 つの国（例：米国）を選択します。
1. **管理者**/**ストア**/**設定**/**顧客**/**顧客設定** に移動し、「**メール確認が必要**」を _はい_ に設定します。
1. **管理者** / **マーケティング** / **メールテンプレート** で新しいメールテンプレートを作成し、テンプレート `Footer (magento/luma)` 読み込んで、テンプレートのコンテンツをCMS ブロックに置き換えます。

   ```CMS
   {{block class="Magento\Cms\Block\Block" block_id="footer_links_block"}}
   ```

1. **管理者**/**コンテンツ**/**デザイン**/**設定** に移動し、フロントエンド web サイトに関連するテーマを選択します。 「フッターテンプレート」に、作成した新しいメールテンプレートを設定します。
1. フロントエンドに移動し、商品を買い物かごに追加します。
1. 顧客を作成すると、メールアドレスを確認するメールが届きます。 確認リンクをクリックします。 Web サイトにログインします。
1. **マイアカウント** に移動し、アドレスを追加します。 住所の国を、以前に管理者設定で設定した配送先国に設定します。
1. チェックアウトに移動します。

<u> 期待される結果 </u>:

お客様の住所が配送先国に対応しているため、配送方法が利用可能です。

<u> 実際の結果 </u>:

発送方法はご利用いただけません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
