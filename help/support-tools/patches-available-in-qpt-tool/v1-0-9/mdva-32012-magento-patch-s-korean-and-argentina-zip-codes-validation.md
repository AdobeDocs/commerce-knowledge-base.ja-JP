---
title: 'MDVA-32012 パッチ：韓国およびアルゼンチンの郵便番号の検証'
description: MDVA-32012 パッチは、アルゼンチンと韓国の郵便番号の変更やバリエーションにより、郵便番号が検証されない問題を解決します。 韓国の郵便番号は 5 桁にする必要がありますが、以前は 6 桁でした。 アルゼンチンの郵便番号は、数字と英数字の両方にすることができます。 MDVA-32012 パッチは、これらの郵便番号の形式がこれらの国で検証されることを意味します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.9 がインストールされている場合に利用できます。 この問題はAdobe Commerce バージョン 2.4.2 で修正される予定であることに注意してください。
exl-id: 9602f50d-6acd-4724-9734-6aeb65393a25
feature: Communications
role: Admin
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# MDVA-32012 パッチ：韓国およびアルゼンチンの郵便番号の検証

MDVA-32012 パッチは、アルゼンチンと韓国の郵便番号の変更やバリエーションにより、郵便番号が検証されない問題を解決します。 韓国の郵便番号は 5 桁にする必要がありますが、以前は 6 桁でした。 アルゼンチンの郵便番号は、数字と英数字の両方にすることができます。 MDVA-32012 パッチは、これらの郵便番号の形式がこれらの国で検証されることを意味します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.9 がインストールされています。 この問題はAdobe Commerce バージョン 2.4.2 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

* このパッチは、クラウドインフラストラクチャー 2.3.5 上のAdobe Commerce用に設計されました。
* また、このパッチは、クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.3.0 ～ 2.4.1 のAdobe Commerce バージョンとも互換性があります。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

韓国語またはアルゼンチン語の英数字を 5 桁の郵便番号を入力すると、次の警告が表示されます。

*入力された郵便番号は無効のようです。 例： [1234 （英数字のアルゼンチン アドレスを入力した場合）] または [123-456 （5 桁の韓国人住所を入力した場合）]. それが正しいと信じる場合は、この通知を無視できます。*

<u>再現手順</u>:

1. ストアフロントを開きます。
1. カートにアイテムを追加します。
1. チェックアウトのプロセス。
1. 国として「韓国」を使用して新しい住所を追加し、5 桁の郵便番号を入力するか、国として「アルゼンチン」を使用して新しい住所を追加し、英数字の郵便番号を入力します。
1. 保存してみてください。

<u>期待される結果</u>:

住所は警告なしで保存する必要があります。

<u>実際の結果</u>:

アドレスを保存すると警告が返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
