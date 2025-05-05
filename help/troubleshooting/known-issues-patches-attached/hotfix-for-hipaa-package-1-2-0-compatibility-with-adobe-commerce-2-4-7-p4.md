---
title: Adobe Commerce 2.4.7-p4.1 [!DNL HIPAA] 2.0 互換性パッケージのホットフィックス
description: この記事では、Cloud Infrastructure 2.4.7 [!DNL HIPAA] p4 上のAdobe Commerceと新しいパッケージ 1.2.0 の互換性を追加するためのホットフィックスを提供します。
feature: Install, Upgrade, Security, Compliance
role: Developer
source-git-commit: 705c43d2328d47fb5f00ae582a2a623ca9f94f70
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Adobe Commerce 2.4.7-p4 [!DNL HIPAA] 1.2.0 互換性パッケージのホットフィックス

この記事では、Cloud Infrastructure 2.4.7-p4 上のAdobe Commerceと **新しい**&#x200B;[!DNL HIPAA] パッケージ 1.2.0 の互換性を追加するためのホットフィックスを提供します。

この問題は、バージョン 2.4.7-p5 リリースで修正される予定です。

## 影響を受けるバージョンと製品

Cloud Infrastructure 2.4.7-p4 以前のAdobe Commerce

## 前提条件

* Adobeは、**[!DNL HIPAA Ready]** 拡張機能にアクセスするためのAdobe Commerce アカウントをプロビジョニングしています。 詳しくは、**Adobe Commerce：はじめる前に [&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) の [!DNL HIPAA] Adobe Commerceへの対応** を参照してください。
* [repo.magento.com](https://repo.magento.com) にアクセスして拡張機能をインストールします。 キーの生成と必要な権限の取得については、**Adobe Commerce: インストールガイド [&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) の  認証キーの取得** を参照してください。

## 問題

[!DNL HIPAA] パッケージ 1.1.0 は、Adobe Commerce 2.4.7x のリリースラインと互換性がありません。

## 解決策

このホットフィックスを通じて、Cloud Infrastructure 2.4.7-p4 でAdobe Commerceを実行しているマーチャントは、[!DNL HIPAA] パッケージ 1.2.0 を使用できます。

>[!NOTE]
>
>**[!DNL HIPAA]1.2.0 は、Adobe Commerce 2.4.7-p5 とのみ互換性があります。 [!DNL HIPAA] 1.2.0 との互換性をAdobe Commerce 2.4.7-p4 に追加する場合は、提供されたパッチをインストールしてください。<br><u>Adobe Commerce 2.4.7-p4 を使用していない場合、このパッチを使用するには、最初にAdobe Commerce 2.4.7-p4 にアップグレードする必要があります </u>。**

Cloud Infrastructure 2.4.7-p4 上のAdobe Commerceの問題を修正するには、パッチを適用する必要があります。

[ac-13382--patch-for-hipaa-2-4-7-p4-composer-patch.zip](assets/ac-13382--patch-for-hipaa-2-4-7-p4-composer-patch.zip)

## パッチの適用方法

ファイルを解凍し、サポートナレッジベースの [Adobeが提供する Composer パッチの適用方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-apply-a-composer-patch-provided-by-magento.html?lang=ja) を参照してください。

## Adobe Commerce on Cloud マーチャントの場合のみ – パッチが適用されているかどうかを確認する方法

問題にパッチが適用されたかどうかを簡単に確認することはできないので、そのパッチが正常に適用されたかどうかを確認することをお勧めします。

>[!NOTE]
>
><u> これを行うには、ファイル `VULN-27015-2.4.7_COMPOSER.patch` を使用して、次の手順に従います **例として**</u>。

1. [ 品質向上パッチツールのインストール ](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja)。
1. 次のコマンドを実行します。<br>
   ![cve-2024-34102-tell-if-patch-applied-code](assets/cve-2024-34102-tell-if-patch-applied-code.png)
1. 次のような出力が表示されます **<u>ここで使用した例では、VULN-27015</u>** は *Applied* ステータスを返します。

   ```bash
   ║ Id            │ Title                                                        │ Category        │ Origin                 │ Status      │ Details                                          ║ ║ N/A           │ ../m2-hotfixes/VULN-27015-2.4.7_COMPOSER_patch.patch      │ Other           │ Local                  │ Applied     │ Patch type: Custom                                
   ```

<!-- For Step 2:
     ```bash
    vendor/bin/magento-patches -n status |grep "27015\|Status"
     ```
-->
