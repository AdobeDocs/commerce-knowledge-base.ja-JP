---
title: Adobe Commerceでセキュリティ更新プログラムを利用できます – [!DNL APSB24-73]
promoted: true
description: Adobe Commerce 2.4.7-p3、2.4.6 [!DNL critical, important, and moderate vulnerabilities] p8、2.4.5-p10、2.4.4-p11 およびそれ以前のバージョンのインスタンスのみを実行している場合は、個別パッチを適用して修正し  [!DNL B2B]  す。
feature: Compliance, Security
role: Developer
source-git-commit: 181316dc0bd42feae0a857ff52edd80dbfd492ad
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Adobe Commerceでセキュリティ更新プログラムを利用できます – [!DNL APSB24-73]

2024 年 10 月 8 日（PT）に、Adobeは、Adobe Commerce、Magento Open Sourceおよび [!DNL Adobe Commerce Webhooks Plugin] のセキュリティ更新を定期的にスケジュールしてリリースしました。
この更新により、[[!DNL critical, important] および  [!DNL moderate]](https://helpx.adobe.com/security/severity-ratings.html) の脆弱性が解決されます。 不正利用に成功すると、任意のコードの実行、任意のファイルシステムの読み取り、セキュリティ機能のバイパス、権限のエスカレーションが発生する可能性があります。 掲示板は [Adobeセキュリティ速報（[!DNL APSB24-73]） ](https://helpx.adobe.com/security/products/magento/apsb24-73.html) です。

>[!NOTE]
>
>上記のセキュリティ速報に記載されている **[!DNL CVE-2024-45115]は、[!DNL B2B] モジュールを使用する場合にのみ適用されます。** この脆弱性に対する修正をできる限り迅速に適用できるように、Adobeでは、[!DNL CVE-2024-45115] れを解決する分離パッチもリリースしました。

**最新のセキュリティ更新プログラムを早急に適用してください。 そうしないと、これらのセキュリティ上の問題に対して脆弱になり、Adobeは修正を支援する手段が限られてしまいます。**

>[!NOTE]
>
>セキュリティパッチ/分離パッチの適用で問題が発生した場合は、サポートサービスにお問い合わせください。

## 影響を受ける製品とバージョン

Adobe Commerce on Cloud、Adobe Commerce オンプレミスおよびMagento Open Source:

* 2.4.7-p3 以前
* 2.4.6-p8 以前
* 2.4.5-p10 以前
* 2.4.4-p11 以前

## Adobe Commerce on Cloud、Adobe Commerce オンプレミスのソフトウェアおよびMagento Open Sourceのソリューション

影響を受ける製品およびバージョンの脆弱性を解決するには、[!DNL CVE-2024-45115] Isolated パッチを適用する必要があります。

## 個別パッチの詳細

アタッチされた分離パッチを使用します。

[vuln-25610-composer-patch.zip](assets/vuln-25610-composer-patch.zip)

## 分離パッチの適用方法

ファイルを解凍し、サポートナレッジベースで [Adobe提供の Composer パッチの適用方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html) を参照して手順を確認します。

## Adobe Commerce on Cloud マーチャントの場合のみ – 分離パッチが適用されているかどうかを確認する方法

問題にパッチが適用されたかどうかを簡単に確認することはできないので、[!DNL CVE-2024-45115] Isolated パッチが正常に適用されたかどうかを確認することをお勧めします。

<u> これを行うには、ファイル `VULN-27015-2.4.7_COMPOSER.patch` を使用して、次の手順を実行します **例として**</u>。

1. [ 品質向上パッチツールのインストール ](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html)。
1. 次のコマンドを実行します。<br>
   ![cve-2024-34102-tell-if-patch-applied-code](assets/cve-2024-34102-tell-if-patch-applied-code.png)
1. VULN-27015 が *Applied* ステータスを返す、次のような出力が表示されます。

   ```bash
   ║ Id            │ Title                                                        │ Category        │ Origin                 │ Status      │ Details                                          ║ ║ N/A           │ ../m2-hotfixes/VULN-27015-2.4.7_COMPOSER_patch.patch      │ Other           │ Local                  │ Applied     │ Patch type: Custom                                
   ```

<!-- For Step 2:
     ```bash
    vendor/bin/magento-patches -n status |grep "27015\|Status"
     ```
-->

## セキュリティの更新

Adobe Commerceで利用できるセキュリティ更新プログラム：

* [Adobeセキュリティ速報（[!DNL APSB24-73]） ](https://helpx.adobe.com/security/products/magento/apsb24-73.html)
