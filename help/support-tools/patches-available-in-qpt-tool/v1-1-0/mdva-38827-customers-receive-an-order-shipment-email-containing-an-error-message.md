---
title: 「MDVA-38827：顧客がメールで注文出荷エラーを受信する」
description: 「MDVA-38827 パッチは、次のエラーメッセージが記載された注文出荷メールが顧客に届く問題を修正します。*申し訳ありません。このコンテンツの生成中にエラーが発生しました*。 このパッチは、[Quality Patches Tool （QPT） ] （https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/patches/overview） 1.1.0 がインストールされている場合に利用できます。 パッチ ID は MDVA-38827。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。」
exl-id: f2e5aeab-7d46-46be-9631-c3a863d9bf52
feature: Communications, Marketing Tools, Orders, Shipping/Delivery
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# MDVA-38827：顧客がメールで注文出荷エラーを受信する

MDVA-38827 パッチは、次のエラーメッセージが記載された注文出荷メールが顧客に届く問題を修正します。*申し訳ありません。このコンテンツの生成中にエラーが発生しました*。 このパッチは、[Quality Patches Tool （QPT） ](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/patches/overview)1.1.0 がインストールされている場合に使用できます。 パッチ ID は MDVA-38827。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.3-p1 - 2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

出荷について「メールで顧客に通知」オプションを選択すると、顧客は次のエラーメッセージを含むメールを受け取ります。*申し訳ありません。このコンテンツの生成中にエラーが発生しました*。

<u> 再現手順 </u>:

1. **マーケティング**/**コミュニケーション**/**メールテンプレート** に移動し、「**新しいテンプレートを追加**」を選択します。
   * **Magento売上** / **新規出荷** を選択します。
   * 「**テンプレートを読み込み**」をクリックします。
   * テンプレート名（コアシッピングテンプレートなど）を追加し、「**保存**」をクリックします。
1. **Store**/設定/**構成**/**Sales**/**Sales Email** に移動します。
   * **出荷注釈** を有効にします。
   * ゲストの出荷コメントメールテンプレートおよび出荷コメントメールテンプレートで、「**コア出荷テンプレート**」（手順 1 の「テンプレート名の追加」の部分を参照）を選択します。
1. 注文します。 管理パネル/**営業**/**注文** に移動し、「**表示**」をクリックして注文を出荷します。
1. 注文の状態が「保留」から「処理中」に変わります。
1. 左側のサイドバーメニューで **出荷** をクリックし、**表示** をクリックして注文を確認します。
1. **出荷履歴** の下の **コメントテキスト** にコメントを追加し、「**メールで顧客に通知**」チェックボックスをオンにします。
1. **コメントを送信** をクリックします。

<u> 期待される結果 </u>:

出荷コメント付きの販売メールが生成されます。

<u> 実際の結果 </u>:

メールに次のエラーメッセージが表示されます：*申し訳ありません。このコンテンツの生成中にエラーが発生しました。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
