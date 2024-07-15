---
title: 管理者アクセスが制限され、パフォーマンスの問題が発生する
description: この記事では、ユーザーガイドの [Web サイトによって役割の範囲が制限されている管理者の役割 ] （https://docs.magento.com/m2/ee/user_guide/system/permissions-user-roles.html#step-2assign-resources）を使用することでパフォーマンスに悪影響が出た場合の解決策について説明します。
exl-id: da168d6b-9cda-41e2-aa3c-f3f0dccc803d
feature: Admin Workspace, Cache
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 管理者アクセスが制限され、パフォーマンスの問題が発生する

この記事では、ユーザーガイドで [web サイトによって役割の範囲が制限されている管理者の役割 ](https://docs.magento.com/m2/ee/user_guide/system/permissions-user-roles.html#step-2assign-resources) を使用することでパフォーマンスに悪影響が出る場合の解決策を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.2.x、2.3.x
* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x

## 問題

Web サイトによってロール範囲が制限されている管理者ユーザーが管理パネルで操作（ログイン、商品の保存など）を行うと、Adobe Commerceは保存されているキャッシュを再構築します。 キャッシュの再構築はパフォーマンスに悪影響を及ぼし、特に営業時間内やトラフィック量が多い時間帯にサイトの停止につながる可能性があります。

この問題は、Adobe Commerce 2.2.10 および 2.3.3 で修正されました。

## 解決策

この問題を回避するオプションを次に示します。

* Adobe Commerce アプリケーションのバージョンを 2.2.10 または 2.3.3 にアップグレードします。 （手順については、開発者向けドキュメントの [ クラウドインフラストラクチャー上のAdobe Commerceのバージョンのアップグレード ](https://devdocs.magento.com/guides/v2.3/cloud/project/project-upgrade.html) を参照してください。
* 可能であれば、管理者ユーザーの役割の範囲を web サイトで制限しないでください。
* [Magentoサポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) して、パッチをリクエストします（使用可能な場合）。

## 関連資料

* ユーザーガイドの [ ユーザーの役割 ](https://docs.magento.com/m2/ee/user_guide/system/permissions-user-roles.html)。
