---
title: 「MDVA-39605:Redis キャッシュ TTL （有効期限）の値が間違っている」
description: MDVA-39605 パッチは、Redis キャッシュ TTL （有効期限）の値が間違っている問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.13 がインストールされている場合に利用できます。 パッチ ID は MDVA-39605。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 7283838b-702d-4ddc-aa03-829dbf5aa91f
feature: Cache, Console, Services
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# MDVA-39605: Redis キャッシュ TTL （有効期限）の値が間違っています

MDVA-39605 パッチは、Redis キャッシュ TTL （有効期限）の値が間違っている問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.13 がインストールされている場合に使用できます。 パッチ ID は MDVA-39605。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Redis キャッシュ TTL （有効期限）の値が間違っています。

<u> 再現手順 </u>:

修正をテストするには、キャッシュをフラッシュして、ストアフロントで設定可能な製品を開きます。 次に、ターミナル（コンソール）を開き、次の手順に従います。

1. コマンド `redis-cli` を実行します。
1. `KEYS "*PRICE"` を実行します（結果には、例えば `zc:ti:e54_PRICE` などのキーが 1 つだけ含まれている必要があります）。 キーをコピーします。
1. `SMEMBERS` を実行し、その後に前の手順のキー（例：`SMEMBERS zc:ti:e54_PRICE`）を実行します。 結果から任意のキーをコピーします（例：e54_4E67B390D5C28FC7C3D9BB0D37AB3F7B5E576421）。
1. 前の手順のキー名で `KEYS "*<key>"` を実行して、完全なキー名（例：`KEYS "*e54_4E67B390D5C28FC7C3D9BB0D37AB3F7B5E576421"`）を取得します。 結果にはキーが 1 つだけ含まれます（例：`zc:k:e54_4E67B390D5C28FC7C3D9BB0D37AB3F7B5E576421`）。 お気づきのように、フルキー名はプレフィックス「`zc:k:`」が付いたキー名です。 次に、フルキーの名前をコピーします。
1. 手順 4 で、`HGETALL` に続いて完全なキー名を実行して、値を確認します。 値には、関連する設定可能な商品の関連商品のシリアル化されたデータが含まれている必要があります。
1. 手順 4 で、`TTL` に続いて完全なキー名を実行し、キーに有効期限があるかどうかを確認します。 結果は **-1** および **-2 とは異なり** 約 2592000 （30 日）である必要があります。 コードで設定されている有効期限は 1 年ですが、Adobe Commerceで使用される Redis ライブラリの有効期限はハード最大有効期限が 2592000 秒です。

<u> 期待される結果 </u>:

有効期限は 2592000 秒です

<u> 実際の結果 </u>:

有効期限は **-1** または **-2** に設定されています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
