---
title: 最新のAdobe Commerce プレリリースにアクセスできない
description: この記事では、Adobe Commerceの最新のプレリリースコードを利用する際の問題に対する解決策を提供します。
exl-id: cbf54a15-b307-4bfc-90b7-cff98aeb4fce
feature: Roles/Permissions
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---

# 最新のAdobe Commerce プレリリースにアクセスできない

この記事では、Adobe Commerceの最新のプレリリースコードを利用する際の問題に対する解決策を提供します。

>[!NOTE]
>
>Betaへのアクセスに問題がある場合は、[最新のBeta バージョンにアクセスできません](/help/how-to/general/cannot-access-the-latest-beta-version.md)の記事を参照してください。

## イシュー

この記事では、プレリリースコードへのアクセスに関する次の問題について説明します。

* プレリリースコードが見つかりません。
* Composerを使用して[magento.com](https://account.magento.com/customer/account/login)から早期アクセスのAdobe Commerce バージョンをダウンロードできませんでした。

## 原因

問題の最も一般的な原因は次のとおりです。

* 早期アクセスコードを間違った場所で探しています。
* Composerを介してコードにアクセスする際に、間違ったMageIDを使用している。
* あなたのアカウントはプレリリースプログラムに含まれていません。

## Solution

### 早期アクセスコードの場所

プレリリースの間、リリースパッケージは2つの場所で利用できます。

1. アカウントのプライマリ MageIDを使用して、[magento.com](https://repo.magento.com/)のComposer経由で行います。 Composerの使用方法について詳しくは、開発者向けドキュメントの「[Composerを使用したAdobe Commerceのインストール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/composer)」を参照してください。
1. [account.magento.com](https://account.magento.com/customer/account/login)の&#x200B;**マイアカウント** > **ダウンロード**。

>[!NOTE]
>
>リリースパッケージは、GA日までGitHubでは利用できません。

### 使用する必要があるMageID

Adobe Commerceまたはパートナーアカウントに関連付けられているプライマリ MageIDを使用する必要があります。 プレリリースプログラムは、共有アクセス権を持つ連絡先にはリンクされません。 早期アクセスは、Adobe Commerce ライセンスまたはパートナーライセンスに関連付けられているMageIDによって、Composerまたは[repo.magento.com](https://repo.magento.com/)経由でのみアクセスできます。

#### 自分のMageIDがプライマリ IDであるかどうかを確認するにはどうすればよいですか？

**マーチャント向け**

MageIDがプライマリであるかどうかを確認するには、次の手順を実行します。

1. [magento.com](https://account.magento.com/customer/account/login)にログインし、**製品とサービス** タブに移動します。 Adobe Commerceのライセンス情報が表示されているかどうかを確認します。
   * Adobe Commerceのライセンス情報が表示された場合は、MageIDがプライマリになります。
   * Adobe Commerceのライセンス情報が表示されない場合、MageIDには共有アクセス権のみが付与されます。 プライマリ ID所有者が誰であるかを確認するには、**自分と共有**&#x200B;に移動します。ここで指定した共有名に注意してください。 「**アカウントを切り替え**」をクリックし、SHARENAMEに記録した値を選択します。 ようこそページには、プライマリ ID所有者の電子メールが表示されます。
1. 何らかの理由で[magento.com](https://account.magento.com/customer/account/login)でこの情報が見つからない場合は、Adobeのアカウントチームにお問い合わせください。
1. 上記のいずれも機能しない場合は、[ サポートにお問い合わせください](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)。

**パートナー向け**

MageIDがプライマリであるかどうかを確認するには、次の手順を実行します。

1. [magento.com](https://account.magento.com/customer/account/login)にログインし、**製品とサービス** タブに移動します。 「パートナー」サブセクションで、アクティブなパートナーライセンス情報が表示されているかどうかを確認します。
   * アクティブなパートナーライセンス情報が表示された場合、MageIDはプライマリになります。 END DATE値が将来の日付である場合、パートナーライセンスはアクティブです。
   * アクティブなパートナーライセンス情報が表示されない場合、MageIDには共有アクセス権のみが付与されます。 プライマリ ID所有者が誰であるかを確認するには、**自分と共有**&#x200B;に移動します。ここで指定した共有名に注意してください。 「**アカウントを切り替え**」をクリックし、SHARENAMEに記録した値を選択します。 ようこそページには、プライマリ ID所有者の電子メールが表示されます。
1. 何らかの理由で[magento.com](https://account.magento.com/customer/account/login)でこの情報が見つからない場合は、パートナーマネージャーにお問い合わせください。
1. 上記のいずれも機能しない場合は、[ サポートにс連絡してください](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)。

### プレリリースプログラムには含まれていません

プレリリース版のアクセスプログラムに含めるには、組織が良好な状態にあるアクティブなAdobe Commerce アカウントまたはパートナーアカウントを持っている必要があります。 この条件を満たしており、プレリリースコードにアクセスできないと思われる場合は、MageIDで[ サポート ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)にお問い合わせください。
