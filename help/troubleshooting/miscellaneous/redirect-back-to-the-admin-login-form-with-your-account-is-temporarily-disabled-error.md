---
title: 「アカウントが一時的に無効になっています」エラーが表示された状態で、[!UICONTROL Commerce Admin] ログインフォームにリダイレクトします
description: この記事では、次のエラーメッセージが表示されたログインフォームにリダイレクトされるCommerce管理者のログインに関する問題の解決策を紹介します。*「お客様のアカウントは一時的に無効になっています」*。 推奨される解決策は、管理者ユーザーデータベース設定の確認と修正です。
exl-id: 1c7ffa1c-1fb1-4f69-9534-77d1e119318a
feature: Admin Workspace, Customer Service
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: bb2df8be-afdd-4818-b6b5-95ca1dd3bc3a
    internal-label: Admin workspace
  - id: deedbb4d-f1b7-58ea-a34a-de1f481f9d4c
    internal-label: Customer Service
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%
---
# 「アカウントが一時的に無効になっています」エラーが表示された状態で、[!UICONTROL Commerce Admin] ログインフォームにリダイレクトします

この記事では、次のエラーメッセージが表示されたログインフォームにリダイレクトされる[!UICONTROL Commerce Admin] ログインの問題に対する可能な解決策について説明します。*「アカウントが一時的に無効になっています」*。 推奨される解決策は、管理者ユーザーデータベース設定の確認と修正です。

## 影響を受けるエディションとバージョン：

Adobe Commerceのすべてのバージョンとエディション

## イシュー

<u>複製する手順</u>:

1. **[!UICONTROL Commerce Admin]** ページに移動します。
1. 資格情報を入力し、**ログイン**&#x200B;をクリックします。

<u>期待される結果</u>:

[!UICONTROL Commerce Admin]にログインします。

<u>実際の結果</u>:

ログインフォームにリダイレクトされ、次のエラーメッセージが表示されます。*「アカウントは一時的に無効になっています。 後でもう一度やり直してください&quot;*。

## Solution

1. データベースのバックアップを作成します。
1. [[!DNL phpMyAdmin]](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/optional-software#phpmyadmin)などのデータベースツールを使用するか、コマンドラインからDBに手動でアクセスします。 `admin_user` データベース テーブルで、管理者ユーザーレコードの`is_active`が「`1`」に設定されており、`lock_expires`が`NULL`であるかどうかを確認します。 必要に応じて、これらの値をリセットします。

## 関連トピックス

* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
