---
title: 「ACSD-51892：設定ファイルが複数回読み込まれるパフォーマンスの問題」
description: ACSD-51892 パッチを適用して、のデプロイメント中に設定ファイルが複数回読み込まれるAdobe Commerceのパフォーマンスの問題を修正してください。
feature: Observability
role: Admin
exl-id: 397343df-360f-43c4-bcef-be5f0da5aeef
source-git-commit: 97734799a39f41d0d6441379e21608fa5fcd1d4c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# ACSD-51892：設定ファイルが複数回読み込まれるパフォーマンスの問題

ACSD-51892 パッチは、1 回のリクエスト内でデプロイメント設定値にアクセスするたびに `app/etc/env.php` ファイルと `app/etc/config.php` ファイルを読み込むことによって発生するパフォーマンスの問題を修正します。 ファイルの過度の読み取りは、システムに負担をかけ、全体的なパフォーマンスの低下につながります。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-51892 です。 この問題はAdobe Commerce 2.4.6-p2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定ファイルが複数回読み込まれるパフォーマンスの問題があります。

<u> 再現手順 </u>:

1. デプロイメントを実行するか、Adobe Commerce 2.4.6 以降にアップグレードします。
1. デプロイメントの実行中にファイルシステムのログを調べて、`app/etc/env.php` ファイルや `app/etc/config.php` ファイルへのアクセスを確認します。

<u> 期待される結果 </u>:

デプロイメントは通常の期間内に成功します。

<u> 実際の結果 </u>:

* サーバは、入力したコマンドに応答するのに苦労しています。 この結果、web サイトにアクセスすると、*エラー 503 の最初のバイトがタイムアウト* します。
* ログファイルには、`app/etc/env.php` および `app/etc/config.php` ファイルへのアクセス権を持つ複数のエントリがあります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
