---
title: 「ACSD-53824：セットアップのアップグレードでデプロイメントが失敗する」
description: ACSD-53824 パッチを適用して、セットアップのアップグレード時にデプロイメントが失敗するAdobe Commerceの問題を修正してください
feature: Attributes, Upgrade
role: Admin, Developer
exl-id: a071745f-967f-42c8-9e20-52b248e4fefa
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# ACSD-53824: セットアップのアップグレード時に展開が失敗する

ACSD-53824 パッチは、セットアップのアップグレード時にデプロイメントが失敗する問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.38 がインストールされています。 パッチ ID は ACSD-53824 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 - p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

セットアップのアップグレード時にデプロイメントが失敗します。

<u>再現手順</u>:

1. を使用したインフラストラクチャのインストール **[!DNL MariaDB]** （Galera クラスタ上）
1. を `wsrep_max_ws_size` 最大 *2 GB*.
1. 新しいAdobe Commerce インスタンスをインストールします。
1. 中程度のパフォーマンス プロファイルから器具を生成します。
   `php bin/magento setup:performance:generate-fixtures -s setup/performance-toolkit/profiles/ee/medium.xml`
1. 次を超えて生成 **12000** 複数の属性を選択します。
1. 次に、を使用します `Run setup: Upgrade` コマンド。

<u>期待される結果</u>:

この `setup:upgrade` エラーなしで完了します。

<u>実際の結果</u>:

この `setup:upgrade` 次で失敗 [!DNL MySQL] エラー：

`Allowed memory size of 6442450944 bytes exhausted in ../module-catalog/Setup/Patch/Data/UpdateMultiselectAttributesBackendTypes.php`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
