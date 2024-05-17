---
title: 「ACSD-44591:CAPTCHA 確認なしで注文するとエラーが発生する」
description: ACSD-44591 パッチを使用すると、CAPTCHA の確認なしに注文しようとするとエラーが発生する問題を解決できます。
exl-id: 5459aa14-dcba-474d-aafa-e4cc73daafbc
feature: Orders
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# ACSD-44591:CAPTCHA 確認なしで注文する場合のエラー

ACSD-44591 パッチを使用すると、CAPTCHA の確認なしに注文しようとするとエラーが発生する問題を解決できます。
このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.17 がインストールされています。 パッチ ID は ACSD-44591 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

CAPTCHA 確認を使用せずに注文しようとすると、エラーが発生する。

<u>再現手順</u>:

1. Google ReCaptcha v2 （I&#39;m not a robot）を設定します。
1. チェックアウトの reCaptcha を有効にします。
1. ReCaptcha をクリックせずに注文してみてください。
1. 欠落している ReCaptcha （*ReCaptcha 検証に失敗しました。再試行してください*）、クリックします。 **ReCaptcha** その後、注文してみてください。

<u>期待される結果</u>:

間違った ReCaptcha を使用して注文することはありません。

<u>実際の結果</u>:

次のエラーが発生します。

* *ReCaptcha 検証に失敗しました。再試行してください*
* *ID = 1 のカートがありません*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
