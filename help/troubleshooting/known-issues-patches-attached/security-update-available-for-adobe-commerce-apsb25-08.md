---
title: Adobe Commerceでセキュリティ更新プログラムを利用できます – [!DNL APSB25-08]
promoted: true
description: ' [!DNL critical, important, and moderate vulnerabilities]  Adobe CommerceとMagento Open Source 2.4.7-beta1、2.4.7-p3、2.4.6-p8、2.4.5-p10、2.4.4-p11 およびそれ以前のバージョンの両方に対して、個別パッチを適用して修正します。'
feature: Compliance, Security
role: Developer
source-git-commit: 45c6486dea10b37aa8114467bbd7be0c7f9f86f6
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Adobe Commerceでセキュリティ更新プログラムを利用できます – [!DNL APSB25-08]

2025 年 2 月 11 日（PT）に、Adobeは、Adobe CommerceおよびMagento Open Sourceのセキュリティ更新を定期的にスケジュールしてリリースしました。 この更新により、[[!DNL critical, important] および  [!DNL moderate]](https://helpx.adobe.com/security/severity-ratings.html) の脆弱性が解決されます。 これらの脆弱性が悪用されると、任意のコード実行、セキュリティ機能のバイパス、権限のエスカレーションが発生する可能性があります。 詳しくは、[Adobeセキュリティ速報（[!DNL APSB25-08]）を参照してください ](https://helpx.adobe.com/security/products/magento/apsb25-08.html)。

>[!NOTE]
>
>**上記のセキュリティ速報に記載されている [!DNL CVE-2025-24434] の修正をできるだけ迅速に適用できるように、Adobeは [!DNL CVE-2025-24434] を解決する独立したパッチもリリースしました。 これにより、マーチャントは、統合の問題が発生する可能性があるために遅延が発生するリスクを減らしながら、修正を個別に適用できます。**

**最新のセキュリティ更新プログラムを早急に適用してください。 そうしないと、セキュリティ上の問題に対して脆弱になり、Adobeでは問題をさらに修正するための手段が限られてしまいます。**

>[!NOTE]
>
>セキュリティパッチ/分離パッチの適用で問題が発生した場合は、サポートサービスにお問い合わせください。

## 影響を受ける製品とバージョン

Adobe Commerce on Cloud インフラストラクチャ、Adobe Commerce オンプレミスおよびMagento Open Source:

* 2.4.7-beta1 以前
* 2.4.7-p3 以前
* 2.4.6-p8 以前
* 2.4.5-p10 以前
* 2.4.4-p11 以前

## Adobe Commerce on Cloud およびAdobe Commerceのオンプレミスソフトウェアのソリューション

影響を受ける製品およびバージョンの脆弱性を解決するには、[!DNL CVE-2025-24434] Isolated パッチを適用する必要があります。

## 個別パッチの詳細

アタッチされた分離パッチを使用します。

[vuln-28982-composer-patch.zip](assets/vuln-28982-composer-patch.zip)

## 分離パッチの適用方法

ファイルを解凍し、サポートナレッジベースで [Adobe提供の Composer パッチの適用方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html) を参照して手順を確認します。

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

* [Adobeセキュリティ速報（[!DNL APSB25-08]） ](https://helpx.adobe.com/security/products/magento/apsb25-08.html)
* [Adobe Commerceで利用可能な最新のセキュリティ更新 ](https://helpx.adobe.com/security/products/magento.html)
