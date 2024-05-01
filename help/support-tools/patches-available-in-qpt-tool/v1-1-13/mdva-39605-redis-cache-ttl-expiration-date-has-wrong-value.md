---
title: 「MDVA-39605:Redis キャッシュ TTL （有効期限）の値が間違っている」
description: MDVA-39605 パッチは、Redis キャッシュ TTL （有効期限）の値が間違っている問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.13 がインストールされている場合に利用できます。 パッチ ID は MDVA-39605。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 7283838b-702d-4ddc-aa03-829dbf5aa91f
feature: Cache, Console, Services
role: Admin
source-git-commit: 667fcacd5b6cbf56a5fd919d0683ad6a0f979fca
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# MDVA-39605: Redis キャッシュ TTL （有効期限）の値が間違っています

MDVA-39605 パッチは、Redis キャッシュ TTL （有効期限）の値が間違っている問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.13 がインストールされています。 パッチ ID は MDVA-39605。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Redis キャッシュ TTL （有効期限）の値が間違っています。

<u>再現手順</u>:

修正をテストするには、キャッシュをフラッシュして、ストアフロントで設定可能な製品を開きます。 次に、ターミナル（コンソール）を開き、次の手順に従います。

1. 次のコマンドを実行します。 `redis-cli`.
1. 実行 `KEYS "*PRICE"` （例えば、結果にはキーが 1 つだけ含まれます。 `zc:ti:e54_PRICE`）に設定します。 キーをコピーします。
1. 実行 `SMEMBERS` +、前の手順のキー（例： `SMEMBERS zc:ti:e54_PRICE`）に設定します。 結果から任意のキーをコピーします（例：e54_4E67B390D5C28FC7C3D9BB0D37AB3F7B5E576421）。
1. 実行 `KEYS "*<key>"` 直前の手順で指定したキー名で取得することにより、完全なキー名が得られます（例： `KEYS "*e54_4E67B390D5C28FC7C3D9BB0D37AB3F7B5E576421"`）に設定します。 結果にはキーが 1 つだけ含まれます（例：）。 `zc:k:e54_4E67B390D5C28FC7C3D9BB0D37AB3F7B5E576421`）に設定します。 お気づきのように、フルキー名は単にプレフィックス「」が付いたキー名です`zc:k:`」と入力します。 次に、フルキーの名前をコピーします。
1. 実行 `HGETALL` 手順 4 で取得したフルキー名を使用して値を確認します。 値には、関連する設定可能な商品の関連商品のシリアル化されたデータが含まれている必要があります。
1. 実行 `TTL` 手順 4 で取得した完全なキー名を使用して、キーに有効期限があるかどうかを確認します。 結果は、次とは異なる必要があります **-1** および **-2** とは、約 2592000 （30 日）である必要があります。 コードで設定されている有効期限は 1 年ですが、Adobe Commerceで使用される Redis ライブラリの有効期限はハード最大有効期限が 2592000 秒です。

<u>期待される結果</u>:

有効期限は 2592000 秒です

<u>実際の結果</u>:

有効期限はに設定されています **-1** または **-2**.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
