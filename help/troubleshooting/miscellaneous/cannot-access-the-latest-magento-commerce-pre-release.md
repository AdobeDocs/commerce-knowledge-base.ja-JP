---
title: 最新のAdobe Commerce プレリリースにアクセスできません
description: この記事では、Adobe Commerceの最新のプレリリースコードを利用しようとする際の問題の解決策を説明します。
exl-id: cbf54a15-b307-4bfc-90b7-cff98aeb4fce
feature: Roles/Permissions
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 最新のAdobe Commerce プレリリースにアクセスできません

この記事では、Adobe Commerceの最新のプレリリースコードを利用しようとする際の問題の解決策を説明します。

>[!NOTE]
>
>ベータ版へのアクセスで問題が発生した場合は、を参照してください [最新のベータ版にアクセスできません](/help/how-to/general/cannot-access-the-latest-beta-version.md) 記事。

## 問題

この記事では、プレリリースコードへのアクセスに関する次の問題について説明します。

* プレリリースコードが見つかりません。
* から早期アクセス用Adobe Commerce バージョンをダウンロードできない [magento.com](https://account.magento.com/customer/account/login) Composer を使用します。

## 原因：

問題の最も一般的な原因は次のとおりです。

* 間違った場所にあるアーリーアクセスコードを探しています。
* Composer 経由でコードにアクセスする場合、間違った MageID を使用しています。
* アカウントは、プレリリースプログラムには含まれていません。

## 解決策

### アーリーアクセスコードの場所

プレリリースでは、リリースパッケージは次の 2 つの場所で使用できます。

1. 上の Composer を使用 [magento.com](https://repo.magento.com/) アカウントのプライマリ MageID の使用。 Composer の使用方法の詳細については、を参照してください。 [Composer を使用したAdobe Commerceのインストール](https://devdocs.magento.com/guides/v2.3/install-gde/composer.html) 開発者向けドキュメントを参照してください。
1. **マイアカウント** > **Downloads** 日付： [account.magento.com](https://account.magento.com/customer/account/login).

>[!NOTE]
>
>リリースパッケージは、GA 日まで GitHub で使用できません。

### 使用する MageID

Adobe Commerceまたはパートナーアカウントに関連付けられたプライマリ MageID を使用する必要があります。 プレリリースプログラムは、共有アクセス権を持つ連絡先にリンクされていません。 アーリーアクセスは、Composer または [repo.magento.com](https://repo.magento.com/) :Adobe Commerce ライセンスまたはパートナーライセンスに関連付けられた MageID。

#### 自分の MageID がプライマリかどうかを確認する方法

**商人向け**

MageID がプライマリかどうかを確認するには、次の手順を実行します。

1. にログインします [magento.com](https://account.magento.com/customer/account/login) に移動します **マイ製品およびサービス** タブ。 Adobe Commerce ライセンス情報が表示されているかどうかを確認します。
   * Adobe Commerce ライセンス情報が表示される場合は、MageID が primary です。
   * Adobe Commerce ライセンス情報が表示されない場合は、MageID には共有アクセスのみが付与されます。 プライマリ ID 所有者を確認するには、にアクセスしてください。 **自分と共有** ここで SHARENAME が指定されていることに注意してください。 クリック **アカウントの切り替え** SHARENAME でメモした値を選択します。 ようこそページに、プライマリ ID 所有者のメールが表示されます。
1. 何らかの理由でこの情報が見つからない場合： [magento.com](https://account.magento.com/customer/account/login)Adobeアカウントチームにお問い合わせください。
1. 上記の方法で解決できない場合は、 [サポートに連絡する](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

**パートナー向け**

MageID がプライマリかどうかを確認するには、次の手順を実行します。

1. にログインします [magento.com](https://account.magento.com/customer/account/login) に移動します **マイ製品およびサービス** タブ。 「パートナー」サブセクションで、アクティブなパートナーライセンス情報が表示されているかどうかを確認します。
   * アクティブなパートナーライセンス情報が表示された場合、MageID はプライマリです。 終了日の値が将来の日付の場合、パートナーライセンスはアクティブになります。
   * アクティブなパートナーライセンス情報が表示されない場合、お使いの MageID には共有アクセスのみが付与されます。 プライマリ ID 所有者を確認するには、にアクセスしてください。 **自分と共有** ここで SHARENAME が指定されていることに注意してください。 クリック **アカウントの切り替え** SHARENAME でメモした値を選択します。 ようこそページに、プライマリ ID 所有者のメールが表示されます。
1. 何らかの理由でこの情報が見つからない場合： [magento.com](https://account.magento.com/customer/account/login)パートナー・マネージャにお問い合わせください。
1. 上記の方法で解決できない場合は、 [сコンタクトサポート](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

### プレリリースプログラムに含まれていない

プレリリースアクセスプログラムに含めるには、正常な状態のアクティブなAdobe Commerceまたはパートナーアカウントが必要です。 この条件を満たしていると思われる場合は、プレリリースコードにアクセスできません。 [サポートに連絡する](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) （MageID を使用）。
