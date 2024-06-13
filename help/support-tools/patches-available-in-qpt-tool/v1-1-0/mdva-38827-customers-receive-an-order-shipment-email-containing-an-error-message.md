---
title: 「MDVA-38827：顧客がメールで注文出荷エラーを受信する」
description: 「MDVA-38827 パッチは、次のエラーメッセージが記載された注文出荷メールが顧客に届く問題を修正します。*申し訳ありません。このコンテンツの生成中にエラーが発生しました*。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.0 がインストールされている場合に利用できます。 パッチ ID は MDVA-38827。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。」
exl-id: f2e5aeab-7d46-46be-9631-c3a863d9bf52
feature: Communications, Marketing Tools, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# MDVA-38827：顧客がメールで注文出荷エラーを受信する

MDVA-38827 パッチでは、お客様が次のエラーメッセージを含む注文出荷メールを受け取る問題が修正されています。 *このコンテンツの生成中にエラーが発生しました*. このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.1.0 がインストールされています。 パッチ ID は MDVA-38827。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.3-p1 - 2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

出荷について「メールで顧客に通知」オプションが選択されている場合、顧客は次のエラーメッセージを含むメールを受け取ります。 *このコンテンツの生成中にエラーが発生しました*.

<u>再現手順</u>:

1. に移動 **Marketing** > **通信** > **メールテンプレート** を選択して、 **新規テンプレートを追加**.
   * を選択 **Magento販売** > **新しい出荷**.
   * クリックする **テンプレートの読み込み**.
   * テンプレート名（例：コア出荷テンプレート）を追加し、 **保存**.
1. に移動 **ストア** > 設定 > **設定** > **売上** > **営業 E メール**:
   * Enable （有効） **出荷コメント**.
   * を選択 **コア出荷テンプレート** （手順 1 の「テンプレート名の追加」の部分を参照） ゲストの出荷コメントメールテンプレートおよび出荷コメントメールテンプレートの下にあります。
1. 注文します。 管理パネルに移動します。 **売上** > **順序**&#x200B;を選択し、 **表示**&#x200B;を選択し、注文を出荷します。
1. 注文の状態が「保留」から「処理中」に変わります。
1. クリック **出荷** 左側のサイドバーメニューのをクリックし、 **表示** 注文を確認します。
1. にコメントを追加 **コメント テキスト** 下 **出荷履歴** チェックボックスをオンにします **メールで顧客に通知**.
1. クリック **コメントを送信**.

<u>期待される結果</u>:

出荷コメント付きの販売メールが生成されます。

<u>実際の結果</u>:

メールに次のエラーメッセージが表示されます。 *申し訳ありませんが、このコンテンツの生成中にエラーが発生しました。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
