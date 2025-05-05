---
title: 「MDVA-43201：ロケール PT で DOB フィールドを使用する際にエラーが発生する」
description: MDVA-43201 パッチは、ポルトガル語ロケールの顧客登録フォームで DOB 顧客属性を使用するとエラーが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.10 がインストールされている場合に利用できます。 パッチ ID は MDVA-43201。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 02979378-adc1-4a1a-93bf-a35ad50e6b80
feature: B2B, Cache
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# MDVA-43201：ロケール PT で DOB フィールドを使用する際にエラーが発生する

MDVA-43201 パッチは、ポルトガル語ロケールの顧客登録フォームで DOB 顧客属性を使用するとエラーが発生する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.10 がインストールされている場合に使用できます。 パッチ ID は MDVA-43201。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ポルトガル語ロケール用の DOB 顧客属性が顧客登録フォームに追加されると、フォームにエラーが表示されます *iterator_to_array （）に渡す引数 1 は、指定された null で travesable インターフェイスを実装する必要があります*。

<u> 前提条件 </u>:

B2B モジュールがインストールされている。

<u> 再現手順 </u>:

1. 管理者/**ストア**/**設定**/**一般**/**ロケールオプション** に移動し、「ロケール」を **ポルトガル語（ポルトガル）** に設定して「**保存**」をクリックします。
1. キャッシュの再インデックスとクリア。
1. **ストア**/**属性**/**顧客** に移動します。
1. DOB 顧客属性を開き、**ストアフロントに表示** を **はい** に設定します。
1. **使用するフォーム** からすべてを選択します。
1. 属性を保存します。
1. フロントエンドの新しいアカウントを作成ページに移動します。

<u> 期待される結果 </u>:

ポルトガル語ストアの顧客登録フォームには、DOB 属性の追加に関するエラーはありません。

<u> 実際の結果 </u>:

ポルトガル語ストアの顧客登録フォームで、DOB 属性の追加に関してエラーが発生します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
