---
title: Adobe Commerceでセキュリティ更新プログラムを利用できます – [!DNL APSB25-50]
promoted: true
description: Adobe Commerce 2.4.8、2.4.7 [!DNL critical and important vulnerabilities] p5、2.4.6-p10、2.4.5-p12、2.4.4-p13 およびそれ以前のバージョンに対応する分離パッチを適用します。
feature: Compliance, Security
role: Developer
source-git-commit: 9df7dee77bec7ffe4323f21e44d555338a0b1934
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Adobe Commerceでセキュリティ更新プログラムを利用できます – [!DNL APSB25-50]

2025 年 6 月 10 日（PT）に、Adobeは、Adobe CommerceおよびMagento Open Sourceのセキュリティ更新を定期的にスケジュールしてリリースしました。 この更新により [[!DNL critical]  および  [!DNL important]](https://helpx.adobe.com/jp/security/severity-ratings.html) の脆弱性が解決されます。 これらの脆弱性が悪用されると、セキュリティ機能のバイパス、権限のエスカレーション、任意のコードの実行が発生する可能性があります。

詳しくは、[Adobeのセキュリティ速報（[!DNL APSB25-50]）を参照してください ](https://helpx.adobe.com/security/products/magento/apsb25-50.html)。

>[!NOTE]
>
>**上記のセキュリティ速報に記載されている [!DNL CVE-2025-47110] の修正ができるだけ迅速に適用できるように、Adobeでは [!DNL CVE-2025-47110] れを解決する独立したパッチもリリースしました。 これにより、マーチャントは、統合の問題が発生する可能性があるために遅延が発生するリスクを減らしながら、修正を個別に適用できます。**

**最新のセキュリティ更新プログラムを早急に適用してください。 そうしないと、これらのセキュリティ上の問題に対して脆弱になり、Adobeがこの問題をさらに修正するのに役立つ手段が限られてしまいます。**

[ 個別パッチ導入プロセス ](https://business.adobe.com/blog/introducing-enhanced-security-patch-deployment-and-communications-in-adobe-commerce) の詳細については、こちらを参照してください。

>[!NOTE]
>
>Managed Servicesのお客様のAdobe Commerceの場合、カスタマーサクセスエンジニアからパッチ適用に関する追加ガイダンスを提供できます。

>[!NOTE]
>
>セキュリティパッチ/分離パッチの適用で問題が発生した場合は、サポートサービスにお問い合わせください。

[Adobe Commerceで利用可能な最新のセキュリティ更新プログラムについては、こちらを参照してください ](https://helpx.adobe.com/jp/security/products/magento.html)。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法）:

* 2.4.8
* 2.4.7-p5 以前
* 2.4.6-p10 以前
* 2.4.5-p12 以前
* 2.4.4-p13 以前

## 問題

### I. CVE-2025-47110:Adobe Commerce 2.4.7-p4 のサーバーサイドテンプレートインジェクションを使用した XSS の保存

<u> 影響を受ける製品とバージョン </u>:

Adobe Commerce（すべてのデプロイメント方法）:

* 2.4.8
* 2.4.7-p5 以前
* 2.4.6-p10 以前
* 2.4.5-p12 以前
* 2.4.4-p13 以前

<u> 解決策 </u>:

Adobe Commerce バージョンの場合：

* 2.4.8
* 2.4.7、2.4.7-p1、2.4.7-p2、2.4.7-p3、2.4.7-p4、2.4.7-p5
* 2.4.6、2.4.6-p1、2.4.6-p2、2.4.6-p3、2.4.6-p4、2.4.6-p5、2.4.6-p6、2.4.6-p7、2.4.6-p8、2.4.6-p10
* 2.4.5、2.4.5-p1、2.4.5-p2、2.4.5-p3、2.4.5-p4、2.4.5-p5、2.4.5-p6、2.4.5-p7、2.4.5-p8、2.4.5-p9、2.4.5-p10、2.4.5-p11、2.4.5-p12
* 2.4.4、2.4.4-p1、2.4.4-p2、2.4.4-p3、2.4.4-p4、2.4.4-p5、2.4.4-p6、2.4.4-p7、2.4.4-p8、2.4.4-p9、2.4.4-p10、2.4.4-p11、2.4.4-p12、2.4.4-p12、2.4.4-4-p13

**次の個別パッチを適用するか、最新のセキュリティパッチにアップグレードしてください。**

* **[VULN-31609_2.4.X.patch](assets/VULN-31609_2.4.X_patch.zip)**

### 二 VULN-31547:marketplace.magento.comに XSS が反映+ IMS インスタンスに影響を与えるワンクリック ATO 問題

<u> 影響を受ける製品とバージョン </u>:

Adobe Commerce（すべてのデプロイメント方法）:

* 2.4.8

<u> 解決策 </u>:

Adobe Commerce バージョンの場合：

* 2.4.8

**次の個別パッチを適用するか、最新のセキュリティパッチにアップグレードしてください。**

* **[VULN-31547_2.4.8.patch](assets/VULN-31547_2.4.8_patch.zip)**

## 分離パッチの適用方法

ファイルを解凍し、サポートナレッジベースの [Adobeが提供する Composer パッチの適用方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html?lang=ja) を参照してください。

## Adobe Commerce on Cloud マーチャントの場合のみ – 分離パッチが適用されているかどうかを確認する方法

問題にパッチが適用されたかどうかを簡単に確認することはできないので、[!DNL CVE-2025-47110] の分離されたパッチが正常に適用されたかどうかを確認することをお勧めします。

>[!NOTE]
>
><u> これを行うには、ファイル `VULN-27015-2.4.7_COMPOSER.patch` を使用して、次の手順を実行します **例として**</u>。

1. [ 品質向上パッチツールのインストール ](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja)。
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

* [Adobe セキュリティ速報（[!DNL APSB25-50]） ](https://helpx.adobe.com/security/products/magento/apsb25-50.html)
* [Adobe Commerceで利用可能な最新のセキュリティ更新 ](https://helpx.adobe.com/jp/security/products/magento.html)
