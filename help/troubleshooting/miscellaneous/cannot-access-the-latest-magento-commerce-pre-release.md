---
title: 最新のAdobe Commerce プレリリースにアクセスできません
description: この記事では、Adobe Commerceの最新のプレリリースコードを利用しようとする際の問題の解決策を説明します。
exl-id: cbf54a15-b307-4bfc-90b7-cff98aeb4fce
feature: Roles/Permissions
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 最新のAdobe Commerce プレリリースにアクセスできません

この記事では、Adobe Commerceの最新のプレリリースコードを利用しようとする際の問題の解決策を説明します。

>[!NOTE]
>
>Betaへのアクセスで問題が発生した場合は、[ 最新バージョンのBetaにアクセスできない ](/help/how-to/general/cannot-access-the-latest-beta-version.md) を参照してください。

## 問題

この記事では、プレリリースコードへのアクセスに関する次の問題について説明します。

* プレリリースコードが見つかりません。
* Composer を使用して [magento.com](https://account.magento.com/customer/account/login) からアーリーアクセス Adobe Commerce バージョンをダウンロードできない。

## 原因：

問題の最も一般的な原因は次のとおりです。

* 間違った場所にあるアーリーアクセスコードを探しています。
* Composer 経由でコードにアクセスする場合、間違った MageID を使用しています。
* アカウントは、プレリリースプログラムには含まれていません。

## 解決策

### アーリーアクセスコードの場所

プレリリースでは、リリースパッケージは次の 2 つの場所で使用できます。

1. [magento.com](https://repo.magento.com/) の Composer を介して、アカウントのプライマリ MageID を使用します。 Composer の使用方法について詳しくは、開発者向けドキュメントの [Composer を使用したAdobe Commerceのインストール ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/composer) を参照してください。
1. **マイアカウント**/**ダウンロード**&#x200B;[account.magento.com](https://account.magento.com/customer/account/login)

>[!NOTE]
>
>リリースパッケージは、GA 日まで GitHub で使用できません。

### 使用する MageID

Adobe Commerceまたはパートナーアカウントに関連付けられたプライマリ MageID を使用する必要があります。 プレリリースプログラムは、共有アクセス権を持つ連絡先にリンクされていません。 アーリーアクセスは、Adobe Commerce ライセンスまたはパートナーライセンスに関連付けられた MageID によって、Composer または [repo.magento.com](https://repo.magento.com/) 経由でのみアクセスできます。

#### 自分の MageID がプライマリかどうかを確認する方法

**商人向け**

MageID がプライマリかどうかを確認するには、次の手順を実行します。

1. [magento.com](https://account.magento.com/customer/account/login) にログインし、「製品とサービス **タブに移動** ます。 Adobe Commerce ライセンス情報が表示されているかどうかを確認します。
   * Adobe Commerce ライセンス情報が表示される場合は、MageID が primary です。
   * Adobe Commerce ライセンス情報が表示されない場合は、MageID には共有アクセスのみが付与されます。 プライマリ ID 所有者を確認するには、**自分と共有** に移動します。ここで指定されている SHARENAME に注意してください。 **アカウントの切り替え** をクリックし、SHARENAME でメモした値を選択します。 ようこそページに、プライマリ ID 所有者のメールが表示されます。
1. 何らかの理由でこの情報が [magento.com](https://account.magento.com/customer/account/login) で見つからない場合は、Adobeアカウントチームにお問い合わせください。
1. 上記の方法で解決できない場合は、[ サポートにお問い合わせください ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

**パートナーの場合**

MageID がプライマリかどうかを確認するには、次の手順を実行します。

1. [magento.com](https://account.magento.com/customer/account/login) にログインし、「製品とサービス **タブに移動** ます。 「パートナー」サブセクションで、アクティブなパートナーライセンス情報が表示されているかどうかを確認します。
   * アクティブなパートナーライセンス情報が表示された場合、MageID はプライマリです。 終了日の値が将来の日付の場合、パートナーライセンスはアクティブになります。
   * アクティブなパートナーライセンス情報が表示されない場合、お使いの MageID には共有アクセスのみが付与されます。 プライマリ ID 所有者を確認するには、**自分と共有** に移動します。ここで指定されている SHARENAME に注意してください。 **アカウントの切り替え** をクリックし、SHARENAME でメモした値を選択します。 ようこそページに、プライマリ ID 所有者のメールが表示されます。
1. 何らかの理由でこの情報が [magento.com](https://account.magento.com/customer/account/login) で見つからない場合は、パートナーマネージャーにお問い合わせください。
1. 上記のいずれも機能しない場合は、[ サポートにс連絡してください ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

### プレリリースプログラムに含まれていない

プレリリースアクセスプログラムに含めるには、正常な状態のアクティブなAdobe Commerceまたはパートナーアカウントが必要です。 この条件を満たしていて、プレリリースコードにアクセスできない場合は、MageID を使用して [ サポートにお問い合わせ ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) ください。
