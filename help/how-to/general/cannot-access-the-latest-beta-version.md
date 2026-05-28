---
title: 最新のBeta バージョンにアクセスできない
description: この記事では、最新のBeta バージョンのAdobe Commerce用コードを利用する際の問題に対する解決策を提供します。 Beta コードは、[Adobe Beta プログラム ] （https://github.com/magento/magento2/wiki/Magento-Beta-Program）に記載されているプロセスに従っている公式のAdobe Commerce パートナーでのみ使用できます。
exl-id: a53c854e-38a8-4c8c-8586-9d99c576c835
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# 最新のBeta バージョンにアクセスできない

この記事では、最新のBeta バージョンのAdobe Commerce用コードを利用する際の問題に対する解決策を提供します。 Beta コードは、[Adobe Beta プログラム ](https://github.com/magento/magento2/wiki/Magento-Beta-Program)に記載されているプロセスに従った公式のAdobe Commerce パートナーでのみ使用できます。

## イシュー

この記事では、早期アクセス コードへのアクセスに関する次の問題について説明します。

* Adobe Commerce Beta版は、[magento.com](https://account.magento.com/customer/account/login)の&#x200B;**マイアカウント**/**ダウンロード**&#x200B;の下でダウンロードできません。
* Composerを使用して[magento.com](https://account.magento.com/customer/account/login)から早期アクセスのAdobe Commerce バージョンをダウンロードできませんでした。

## 原因

問題の最も一般的な原因は次のとおりです。

* 早期アクセスコードを間違った場所で探しています。
* 間違ったMageIDを使用しています。
* 開発者には、正しいMageIDからのアクセスキーが必要です。
* お客様のアカウントは、Beta プログラムの一部ではありません。

## Solution

### 早期アクセスコードの場所

ベータアクセス期間中、リリースパッケージは[repo.magento.com](https://repo.magento.com/)のComposerからのみ利用できます。 この間、リリースパッケージはGitHubおよびAdobe Commerce ポータルでは利用できません。これらはGA日にこれらの場所に公開します。 Composerの使用方法について詳しくは、[こちら](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/composer)をクリックしてください。

### 使用する必要があるMageID

パートナーアカウントに関連付けられているプライマリ MageIDを使用する必要があります。 Beta プログラムは、共有アクセス権を持つ連絡先にはリンクされません。 早期アクセスは、パートナーライセンスに関連付けられているMageIDによって、Composerまたは[repo.magento.com](https://repo.magento.com/)経由でのみアクセスできます。

#### 自分のMageIDがプライマリ IDであるかどうかを確認する方法

MageIDがプライマリであるかどうかを確認するには、次の手順を実行します。

1. [magento.com](https://account.magento.com/customer/account/login)にログインし、**製品とサービス** タブに移動します。 「パートナー」サブセクションで、アクティブなパートナーライセンス情報が表示されているかどうかを確認します。
   * アクティブなパートナーライセンス情報が表示された場合、MageIDはプライマリになります。 END DATE値が将来の日付である場合、パートナーライセンスはアクティブです。
   * アクティブなパートナーライセンス情報が表示されない場合、MageIDには共有アクセス権のみが付与されます。 プライマリ ID所有者が誰であるかを確認するには、**自分と共有**&#x200B;に移動します。ここで指定した共有名に注意してください。 「**アカウントを切り替え**」をクリックし、SHARENAMEに記録した値を選択します。 ようこそページに、プライマリ ID所有者の電子メールが表示されます。
1. 何らかの理由で[magento.com](https://account.magento.com/customer/account/login)でこの情報が見つからない場合は、パートナーマネージャーにお問い合わせください。
1. 上記のいずれも機能しない場合は、[ サポートにお問い合わせください](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)。

#### 開発者がキーに正しくアクセスできない

MageIDのプライマリ所有者で、チームの開発者にアクセス権を付与する必要がある場合は、次の手順に従います。

1. プライマリ MageID所有者が[account.magento.com](https://account.magento.com/customer/account/login)にログインします。
1. 「**Marketplace**」タブを選択し、「**アクセスキー**」をクリックします。
1. **新しいアクセスキーを作成**&#x200B;を選択し、名前を付けます。
1. 開発者にキーを送信します。

### 早期アクセスプログラムの一部ではない

アドビのBeta Access プログラムは、アドビのソリューションおよびテクニカルパートナーのみが利用できるため、プリプロダクションのコードを評価できます。 Beta Access プログラムに含めるには、現在の状態が良好で、Beta NDA [ここ](https://github.com/magento/magento2/wiki/Magento-Beta-Program)に署名しているアクティブなAdobe パートナーアカウントが必要です。 これらの条件を満たしており、ベータコードにアクセスできないと思われる場合は、[commercebeta@adobe.com](mailto:commercebeta@adobe.com)にお問い合わせください。
