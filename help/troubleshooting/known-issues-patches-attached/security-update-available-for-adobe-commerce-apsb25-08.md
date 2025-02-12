---
title: Adobe Commerceでセキュリティ更新プログラムを利用できます – [!DNL APSB25-08]
promoted: true
description: Adobe Commerce 2.4.8 [!DNL critical, important, and moderate vulnerabilities] beta1、2.4.7-p3、2.4.6-p8、2.4.5-p10、2.4.4-p11 およびそれ以前のバージョンを修正するための分離パッチを適用します。
feature: Compliance, Security
role: Developer
exl-id: 567e6ad2-704e-461f-a54d-75f6bd96e996
source-git-commit: babb822cc505e2911ae28cd1a2540799146f19b3
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Adobe Commerceでセキュリティ更新プログラムを利用できます – [!DNL APSB25-08]

2025 年 2 月 11 日（PT）に、Adobeは、Adobe CommerceおよびMagento Open Sourceのセキュリティ更新を定期的にスケジュールしてリリースしました。 この更新により、[[!DNL critical, important] および  [!DNL moderate]](https://helpx.adobe.com/security/severity-ratings.html) の脆弱性が解決されます。 これらの脆弱性が悪用されると、任意のコード実行、セキュリティ機能のバイパス、権限のエスカレーションが発生する可能性があります。 詳しくは、[Adobeのセキュリティ速報（[!DNL APSB25-08]）を参照してください ](https://helpx.adobe.com/security/products/magento/apsb25-08.html)。

>[!NOTE]
>
>**上記のセキュリティ速報に記載されている [!DNL CVE-2025-24434] の修正をできるだけ迅速に適用できるように、Adobeでは、[!DNL CVE-2025-24434] を解決する独立したパッチもリリースしました。 これにより、マーチャントは、統合の問題が発生する可能性があるために遅延が発生するリスクを減らしながら、修正を個別に適用できます。**

**最新のセキュリティ更新プログラムを早急に適用してください。 そうしないと、これらのセキュリティ上の問題に対して脆弱になり、Adobeがこの問題をさらに修正するのに役立つ手段が限られてしまいます。**

>[!NOTE]
>
>セキュリティパッチ/分離パッチの適用で問題が発生した場合は、サポートサービスにお問い合わせください。

## 影響を受ける製品とバージョン

Adobe Commerce on Cloud Infrastructure、Adobe Commerce オンプレミス、およびMagento Open Source:

* 2.4.8-beta1 以前
* 2.4.7-p3 以前
* 2.4.6-p8 以前
* 2.4.5-p10 以前
* 2.4.4-p11 以前

## Adobe Commerce on Cloud、Adobe Commerce オンプレミス、Magento Open Source ソフトウェアのソリューション

影響を受ける製品およびバージョンの脆弱性を解決するために、Adobe Commerce/Magento Open Sourceのバージョンに応じて、[!DNL CVE-2025-24434] Isolated パッチを適用する必要があります。

## 個別パッチの詳細

Adobe CommerceまたはMagento Open Sourceのバージョンに応じて、接続されている以下の個別パッチを使用します。

### バージョン 2.4.8-beta1 の場合：

* [vuln-28982-2-4-8x-v2-composer-patch.zip](assets/vuln-28982-2-4-8x-v2-composer-patch.zip)

### バージョン 2.4.7、2.4.7-p1、2.4.7-p2、2.4.7-p3 の場合：

* [vuln-28982-2-4-7x-v2-composer-patch.zip](assets/vuln-28982-2-4-7x-v2-composer-patch.zip)

### バージョン 2.4.6、2.4.6-p1、2.4.6-p2、2.4.6-p3、2.4.6-p4、2.4.6-p5、2.4.6-p6、2.4.6-p7、2.4.6-p8:

* [vuln-28982-2-4-6x-v2-composer-patch.zip](assets/vuln-28982-2-4-6x-v2-composer-patch.zip)

### バージョン 2.4.5、2.4.5-p1、2.4.5-p2、2.4.5-p3、2.4.5-p4、2.4.5-p5、2.4.5-p6、2.4.5-p7、2.4.5-p8、2.4.5-p9、2.4.5-p10:

* [vuln-28982-2-4-5x-v2-composer-patch.zip](assets/vuln-28982-2-4-5x-v2-composer-patch.zip)

### バージョン 2.4.4、2.4.4-p1、2.4.4-p2、2.4.4-p3、2.4.4-p4、2.4.4-p5、2.4.4-p6、2.4.4-p7、2.4.4-p8、2.4.4-p9、2.4.4-p10、2.4.4-p11:

* [vuln-28982-2-4-4x-v2-composer-patch.zip](assets/vuln-28982-2-4-4x-v2-composer-patch.zip)


## 分離パッチの適用方法

ファイルを解凍し、サポートナレッジベースの [Adobeが提供する Composer パッチの適用方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html) を参照してください。

## Adobe Commerce on Cloud マーチャントの場合のみ – 分離パッチが適用されているかどうかを確認する方法

問題にパッチが適用されたかどうかを簡単に確認することはできないので、[!DNL CVE-2025-24434] Isolated パッチが正常に適用されたかどうかを確認することをお勧めします。

>[!NOTE]
>
><u> これを行うには、ファイル `VULN-27015-2.4.7_COMPOSER.patch` を使用して、次の手順を実行します **例として**</u>。

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

* [Adobe セキュリティ速報（[!DNL APSB25-08]） ](https://helpx.adobe.com/security/products/magento/apsb25-08.html)
* [Adobe Commerceで利用可能な最新のセキュリティ更新） ](https://helpx.adobe.com/security/products/magento.html)
