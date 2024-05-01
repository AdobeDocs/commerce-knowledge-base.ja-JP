---
title: 「ファイルは削除できません。 警告！ unlink：からのファイルまたはディレクトリのエラーがありません [!DNL Admin]“
description: この記事では、「ファイルは削除できません」というエラーが表示される問題の解決策を説明します。 警告！unlink そのようなファイルまたはディレクトリが存在しません。エラー* [!DNL Admin] を実行する場合 [!DNL Javascript/CSS] フラッシュ。
feature: Admin Workspace, Observability
role: Developer
exl-id: db265e3c-a809-4404-839a-273001e81d22
source-git-commit: fd5fd6e1bc04db56497a2e0c2a96bc1b06d4f7a1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# *ファイルを削除できません。 警告！unlink：そのようなファイルまたはディレクトリはありませんエラー* から [!DNL Admin]

この記事では、エラーが表示される問題の解決策を説明します *ファイルを削除できません。 警告！unlink：そのようなファイルまたはディレクトリはありませんエラー* から [!DNL Commerce Admin] を実行する場合 [!DNL JavaScript/CSS] フラッシュ。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.0 ～ 2.4.6、すべてのデプロイメント方法

## 問題

を実行するとエラーが発生します [!DNL JS/CSS] フラッシュ :

*「/app/pub/static/_cache/merged/.nfsa42d0e64799fd1000000001b」ファイルは削除できません。 Warning!unlink （/app/pub/static/_cache/merged/.nfsa42d0e64799fd1000000001b）：そのようなファイルまたはディレクトリはありません*

または：に上記のエラーが表示されます。 [!DNL Admin]、または同様のエラー： [!DNL New Relic] またはデプロイメントログで確認できます。

または：高度なレポートにアクセスできず、analytics_collect_data cron ジョブが次のエラーで失敗します。

*「/app/var/tmp/analytics/tmp/.nfsb3b6041dd44588a0000850c0」ファイルは削除できません。 警告！unlink （/app/var/tmp/analytics/tmp/.nfsb3b6041dd44588a0000850c0）：そのようなファイルやディレクトリはありません*

<u>再現手順：</u>

メソッド 1:

1. にログインします [!DNL Admin].
1. に移動 **[!UICONTROL System]** > **[!UICONTROL Cache Management]**.
1. クリック **[!UICONTROL Flush][!DNL JavaScript/CSS][!UICONTROL Cache]**.

メソッド 2:

1. にログインします [!DNL Admin].
1. に移動 **[!UICONTROL Stores]** > *[!UICONTROL Settings]* > **[!UICONTROL Configuration]**.
1. に変更を加えます [!UICONTROL Base URL] または [!UICONTROL Base URL (Secure)].
1. クリックする **[!UICONTROL Save Config]**.

## 解決策

クラウドインフラストラクチャー上のAdobe Commerceで以下を行っている場合： [!DNL magento/magento-cloud-patches] パッチを含む 1.0.22 がインストールされました、あなたは ACSD-50165 を個別にインストールする必要はありません。

Adobe Commerce on Cloud Infrastructure:Commerceのクラウドパッチを 1.0.22 にアップグレード（**またはそれ以降**）が含まれています。これには、この修正が含まれています。 [Commerceのクラウドパッチ](/docs/commerce-cloud-service/user-guide/release-notes/cloud-patches.html).

Adobe Commerce オンプレミス：を使用して ACSD-50165 を適用する [品質向上パッチ 「ツール」 > 「使用方法」](/docs/commerce-operations/tools/quality-patches-tool/usage.html). ACSD-50165 パッチは、に付属しています [!DNL QPT] [v1.1.30](/docs/commerce-operations/tools/quality-patches-tool/release-notes.html#v1-1-30)

## 関連資料

* [[!DNL Quality Patches Tool] > リリースノート](/docs/commerce-operations/tools/quality-patches-tool/release-notes.html) （Commerce ツールガイド）を参照してください。
* [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) （Commerce ツールガイド）を参照してください。
