---
title: 「MC-41359 コマースパッチ：設定 SameSite cookie パラメーターがありません」
description: MC-41359 コマースパッチでは、SameSite cookie パラメーター設定が見つからない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.20 がインストールされている場合に利用できます。 パッチ ID は MC-41359 です。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: b48faa3f-0d9a-4d65-9abb-1573c6240635
feature: Observability
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# MC-41359 コマースパッチ：設定 SameSite cookie パラメーターがありません

MC-41359 コマースパッチでは、SameSite cookie パラメーター設定が見つからない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.20 がインストールされている場合に使用できます。 パッチ ID は MC-41359 です。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.4.2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.6-p1、2.4.2、2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

SameSite cookie パラメーターの設定がありません。

<u> 再現手順：</u>

前提条件：

* Chromeを開き、chrome://flags/に移動します。
* **SameSite のデフォルト Cookie** を有効にし、**SameSite を使用しない Cookie はセキュリティで保護する必要がある** を有効にします。
* Chrome インスペクターを開きます。

<u> シナリオ 1:</u>

1. PayPal を有効にします。
1. 店の前に行きなさい。
1. 商品を買い物かごに追加します。
1. チェックアウトに移動します。

<u> シナリオ 2:</u>

New Relicを有効にしている場合 [ フロントエンドページ ](https://docs.magento.com/user-guide/reports/new-relic-reporting.html) いずれにも警告が表示されます。

<u> 実際の結果：</u>

ブラウザーコンソールの警告メッセージ：*クロスサイトリソースに関連付けられた Cookie が SameSite 属性なしで設定されました。*

<u> 期待される結果：</u>

「lax」は cookie ドメインに追加しないでください。samesite 属性はデフォルト値で存在する必要があります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT ツールで使用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
