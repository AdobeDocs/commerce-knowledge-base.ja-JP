---
title: Adobe Commerceで Cookie の最大数を超えるとエラーが発生する
description: Cookie の最大数を超えるとエラーが発生するAdobe Commerceの問題を解決する方法を説明します。
feature: Deploy, Support, Upgrade, Tools and External Services
role: Admin, Developer
source-git-commit: 44e167c801bbcd313f74c9fc51f9cde9473ef96f
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Adobe Commerceでの *Cookie の最大数を超える可能性があります* エラー

この記事では、Adobe Commerceで *最大数の Cookie を超えてしまいます* というエラーを解決するためのパッチを提供します。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.4 ～ 2.4.7。次のいずれかのパッチが適用されています。

* [[!DNL Quality Patches Tool (QPT)]](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/release-notes) を使用して適用された MDVA-12304 パッチ
* [APSB25-08 分離セキュリティパッチ](/help/troubleshooting/known-issues-patches-attached/security-update-available-for-adobe-commerce-apsb25-08.md)
* [1.1 [!DNL Commerce] 4 用のクラウドパッチ ](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/release-notes/cloud-patches)

## 問題

Adobe Commerceの Cookie に関連する問題が原因で、次のエラーがエラーログに表示されます。

*report.WARNING: Cookie を送信できません。 Cookie の最大数を超えます。*

### 原因：

この問題は、許可される Cookie の最大数が *50* に設定されているので発生します。

## 解決策

1. [!DNL Quality Patches Tool (QPT)] を使用して適用した場合は、MDVA-12304 パッチを削除します。

   * クラウドインフラストラクチャー上のAdobe Commerceの場合は、`.magento.env.yaml` からパッチを削除します。
   * Adobe Commerceのオンプレミス環境の場合は、次のコマンドを実行してパッチを元に戻します。

     `vendor/bin/magento/quality-patches revert MDVA-12304`

1. 使用しているAdobe Commerceのバージョンに応じて、添付されているパッチを適用します。

   * バージョン 2.4.4-p12、2.4.5-p11、2.4.6-p9 および 2.4.7-p4 では、[ACSD-64710 パッチ ](assets/acsd-64710_2.4.5-p11.patch.zip) を適用します。

   * バージョン 2.4.4-p13、2.4.5-p12、2.4.6-p10、2.4.7-p5 および 2.4.8 の場合は、[ACSD-65562 パッチ ](assets/acsd-65562_2.4.5-p12.patch.zip) を適用します。

### 関連資料

* Adobe Commerce アップグレードガイドの [ パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/patches/apply)
* [Adobe Commerce パッチの大規模な配布のベストプラクティス ](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/maintenance/patching-at-scale)Adobe Commerce実装プレイブックに記載
* Commerce on Cloud ガイドの [Commerce Cloud ツールスイートのリリースノート ](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/release-notes/cloud-tools-suite)。
