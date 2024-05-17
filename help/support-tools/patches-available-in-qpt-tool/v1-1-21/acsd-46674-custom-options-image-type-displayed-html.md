---
title: 「ACSD-46674：お客様のメールでHTMLとして表示される画像タイプのカスタムオプション」
description: ACSD-46674 パッチを適用すると、画像タイプのカスタムオプションが顧客のメールでHTMLとして表示されるAdobe Commerceの問題が修正されます。
exl-id: b4941dd0-bb3a-4805-9631-1d256a92f461
feature: Communications, Personalization
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# ACSD-46674：お客様のメールにHTMLとして表示される画像タイプのカスタムオプション

ACSD-46674 パッチを使用すると、画像タイプのカスタムオプションが顧客のメールでHTMLとして表示される問題が修正されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.21 がインストールされています。 パッチ ID は ACSD-46674 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

画像タイプのカスタムオプションは、お客様へのメールでHTMLとして表示されます。

<u>再現手順</u>:

1. カスタムオプションを使用して製品を作成します。
   * オプションの種類： *ファイル*
   * 互換性のあるファイル拡張子： *png, jpg, gif*
   * 必須： *はい*
1. カスタムオプションとしてアップロードされた画像を使用して、この製品を注文します。
1. 手順 2 で作成した注文の請求書を作成します。
1. クレジットメモを作成します。
1. すべての確認メールを確認します。

<u>期待される結果</u>:

確認メールには、アップロードされた画像が表示されます。

<u>実際の結果</u>:

確認メールには、製品のカスタムオプション画像ではなく、プレーンなHTMLコードが含まれています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tools] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

で利用可能なその他のパッチについて [!DNL QPT]を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
