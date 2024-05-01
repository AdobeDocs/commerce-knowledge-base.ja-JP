---
title: 'MDVA-34847:customer_grid_flat テーブルの低速クエリ'
description: MDVA-34847 パッチは、「customer_grid_flat」テーブルで低速クエリが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.16 がインストールされている場合に利用できます。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: e91cb86d-83cd-4267-a132-64465a57da7f
feature: Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# MDVA-34847: customer_grid_flat テーブルの低速クエリ

MDVA-34847 パッチは、で低速クエリが発生する問題を解決します。 `customer_grid_flat` テーブル。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.16 がインストールされています。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.3

**Adobeバージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

低速クエリは次で発生 `customer_grid_flat` テーブル。

<u>再現手順</u>:

1. カスタム範囲を持つ管理者ユーザーの作成（例：設定 **GWS** = *0,* で既存のデフォルト web サイトを選択します **ID** = *1*）に設定します。
1. 製品およびカテゴリ項目を作成します。
1. フロントエンドから注文します。
1. 新しいユーザーとして管理者にログインします。
1. 営業グリッドに移動（**「売上」 > 「受注」**）に設定します。
1. SQL クエリが DB （データベース）に送信されたことを確認します。

<u>期待される結果</u>:

管理 GWS 拡張機能では、を使用する必要があります。

```sql
int
```

の値

```sql
website_id
```

sql 条件で、期待どおりに次のように指定します。

```sql
main_table.website_id IN (1)
```

<u>実際の結果</u>:

Admin GWS 拡張機能によって、という条件が追加されました

```sql
website_id
```

次の値

```sql
string
```

。例：

```sql
main_table.website_id IN ('1')
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
