---
title: '「ファイルは削除できません。 警告！ unlink: [!DNL Admin]」からのファイルまたはディレクトリのエラーはありません。'
description: この記事では、「ファイルは削除できません」というエラーが表示される問題の解決策を説明します。 警告！unlink [!DNL Admin] flush を行う場合、そのようなファイルやディレクトリは存在しません  [!DNL Javascript/CSS]  エラー*。
feature: Admin Workspace, Observability
role: Developer
exl-id: db265e3c-a809-4404-839a-273001e81d22
source-git-commit: fd5fd6e1bc04db56497a2e0c2a96bc1b06d4f7a1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# *ファイルは削除できません。 警告！unlink: [!DNL Admin] からのファイルまたはディレクトリ* エラーがありません

この記事では、「ファイルは削除できません *というエラーが表示される問題の解決策を説明します。 警告！unlink: [!DNL JavaScript/CSS] フラッシュの実行時に [!DNL Commerce Admin] から* そのようなファイルまたはディレクトリのエラーは発生しません。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.0 ～ 2.4.6、すべてのデプロイメント方法

## 問題

[!DNL JS/CSS] フラッシュを実行すると、エラーが発生します。

*「/app/pub/static/_cache/merged/.nfsa42d0e64799fd1000000001b」ファイルは削除できません。 Warning!unlink （/app/pub/static/_cache/merged/.nfsa42d0e64799fd1000000001b）：そのようなファイルやディレクトリはありません*

または：上記のエラーは [!DNL Admin] に表示され、同様のエラーが [!DNL New Relic] またはデプロイメントログに表示されます。

または：高度なレポートにアクセスできず、analytics_collect_data cron ジョブが次のエラーで失敗します。

*「/app/var/tmp/analytics/tmp/.nfsb3b6041dd44588a0000850c0」ファイルは削除できません。 警告！unlink （/app/var/tmp/analytics/tmp/.nfsb3b6041dd44588a0000850c0）：そのようなファイルやディレクトリはありません*

<u> 再現手順：</u>

メソッド 1:

1. [!DNL Admin] にログインします。
1. **[!UICONTROL System]**/**[!UICONTROL Cache Management]** に移動します。
1. **[!UICONTROL Flush][!DNL JavaScript/CSS][!UICONTROL Cache]** をクリックします。

メソッド 2:

1. [!DNL Admin] にログインします。
1. **[!UICONTROL Stores]**/*[!UICONTROL Settings]*/**[!UICONTROL Configuration]** に移動します。
1. [!UICONTROL Base URL] または [!UICONTROL Base URL (Secure)] に変更を加えます。
1. 「**[!UICONTROL Save Config]**」をクリックします。

## 解決策

クラウドインフラストラクチャー上でAdobe Commerceを使用しており、パッチを含む [!DNL magento/magento-cloud-patches] 1.0.22 がインストールされている場合は、ACSD-50165 を別途インストールする必要はありません。

Adobe Commerce on Cloud Infrastructure:Commerceのクラウドパッチを、この修正を含む 1.0.22 （**以降**）にアップグレードします。[Commerceのクラウドパッチ ](/docs/commerce-cloud-service/user-guide/release-notes/cloud-patches.html)。

Adobe Commerce オンプレミス：[Quality Patches Tools > Usage](/docs/commerce-operations/tools/quality-patches-tool/usage.html) を使用して ACSD-50165 を適用します。 ACSD-50165 パッチには、[!DNL QPT] [v1.1.30.](/docs/commerce-operations/tools/quality-patches-tool/release-notes.html#v1-1-30) が付属しています

## 関連資料

* Commerce ツールガイドの [[!DNL Quality Patches Tool] > リリースノート ](/docs/commerce-operations/tools/quality-patches-tool/release-notes.html)。
* [[!DNL Quality Patches Tool]: Commerce ツールガイドのパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) 検索します。
