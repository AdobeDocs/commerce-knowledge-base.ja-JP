---
title: Core Adobe Commerce Payment Integrations の償却
description: 支払いサービス指令PSD2 （[ 支払いサービス指令 ] （https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/payments/compliance-payment-services-directive.html）の詳細を参照）および多くの API の継続的な進化により、Adobe Commerceのコア支払い統合の多くは時代遅れになり、将来的にセキュリティへの準拠を失うリスクがあります。 そのため、多くのコア支払い統合は既に廃止されているか、まもなく廃止される予定です。対応するCommerce Marketplace拡張機能への移行をお勧めします。 支払い統合の最近の非推奨（廃止予定）を確認するには、以下の残りの記事を参照してください。 各**ステータス**リンクはアドビのユーザーガイドに記載されています。 **以下の統合機能はすべてAdobe Commerce 2.4.0 リリースから削除され、2.3 のバージョンから廃止されます。**
exl-id: c2c4b3b6-409d-466f-a4f3-dfe13ac7f972
feature: Compliance, Integration
source-git-commit: f11c8944b83e294b61d9547aefc9203af344041d
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Core Adobe Commerce Payment Integrations の償却

支払サービス指令PSD2 （詳細を参照） [支払サービス指令](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/payments/compliance-payment-services-directive.html) ユーザーガイド）と多くの API の継続的な進化により、Adobe Commerceのコア支払い統合の多くが時代遅れになり、将来セキュリティへの準拠が失われるリスクがあります。 そのため、多くのコア支払い統合は既に廃止されているか、まもなく廃止される予定です。対応するCommerce Marketplace拡張機能への移行をお勧めします。 支払い統合の最近の非推奨（廃止予定）を確認するには、以下の残りの記事を参照してください。 各 **ステータス** リンクはユーザーガイドにあります。 **以下の統合はすべてAdobe Commerce 2.4.0 リリースから削除され、2.3 のバージョンから非推奨（廃止予定）になりました。**

<table style="height: 243px;" width="712">
<tbody>
<tr>
<td style="width: 225.455px;"><strong>支払い方法の統合</strong></td>
<td style="width: 226.364px;"><strong>ステータス</strong></td>
<td style="width: 226.364px;"><strong>Adobe Commerce 2.X の推奨事項</strong></td>
</tr>
<tr>
<td style="width: 225.455px;">Worldpay</td>
<td style="width: 226.364px;">2.3.x - <a href="https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=en#recommended-solutions">2.3.5 以降で非推奨</a><br>2.4.0 – 完全に削除されます</td>
<td style="width: 226.364px;">PSD2 の要件に準拠するために推奨するソリューションを支払いプロバイダーに問い合わせてください。</td>
</tr>
<tr>
<td style="width: 225.455px;">Authorize.net</td>
<td style="width: 226.364px;">2.3.x - <a href="https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=en#recommended-solutions">2.3.4 以降で非推奨</a><br>2.4.0 – 完全に削除されます</td>
<td style="width: 226.364px;">の使用 <a href="https://marketplace.magento.com/authorizenet-magento-module-authorizenet.html">公式の延長</a> 代わりにCommerce Marketplaceから。</td>
</tr>
<tr>
<td style="width: 225.455px;">Authorize.net （Direct Post）</td>
<td style="width: 226.364px;">2.3.x - <a href="https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=en#recommended-solutions">2.3.1 以降で非推奨</a><br>2.4.0 – 完全に削除されます</td>
<td style="width: 226.364px;">の使用 <a href="https://marketplace.magento.com/authorizenet-magento-module-authorizenet.html">公式の延長</a> 代わりにCommerce Marketplaceから。</td>
</tr>
<tr>
<td style="width: 225.455px;">CyberSource</td>
<td style="width: 226.364px;">2.3.x - <a href="https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=en#recommended-solutions">2.3.3 以降で非推奨</a><br>2.4.0 – 完全に削除されます</td>
<td style="width: 226.364px;">の使用 <a href="https://marketplace.magento.com/cybersource-global-payment-management.html">公式の延長</a> 代わりにCommerce Marketplaceから。</td>
</tr>
<tr>
<td style="width: 225.455px;">eWay</td>
<td style="width: 226.364px;">2.3.x - <a href="https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=en#recommended-solutions">2.3.3 以降で非推奨</a><br>2.4.0 – 完全に削除されます</td>
<td style="width: 226.364px;">PSD2 の要件に準拠するために推奨するソリューションを支払いプロバイダーに問い合わせてください。</td>
</tr>
</tbody>
</table>

**PayPal コア支払い方法の統合は非推奨または削除されず、2.3.x および 2.4.x のすべてのリリースで引き続きサポートされることに注意してください。**

## 今後の支払いを安全に保つ方法

Adobe CommerceとMagento Open Sourceのデプロイメントで、非推奨（廃止予定）の支払い統合を引き続き使用している場合は、以下の推奨事項に従って、お客様の支払いが安全で、支払いが拒否されていないことを確認し、Adobe Commerce 2.4.0 へのアップグレードに備えてください。

* から公式の支払い方法拡張機能をインストールして設定します [Commerce Marketplace](https://marketplace.magento.com/extensions/payments-security/payment-integration.html?_ga=2.108129217.2105547619.1564067043-238341041.1564067043) 前述の表で説明したとおり。
* 管理（セット）で非推奨の支払統合を無効にする **Enabled** 設定オプションをに *不可* ）に設定されているため、支払いオプションとしてストアフロントに表示されなくなりました。 新しい注文には、必ず拡張機能の統合を通じて支払いが行われるようにしてください。
* Commerce Marketplaceからの新しい統合は、非推奨の支払い統合を使用して行われた支払い取引を処理できないので、すでに転記済みの取引の完了と払い戻しの可能性がある場合にのみ、両方の支払い方法を並行して使用することをお勧めします。 そのためには、非推奨（廃止予定）のお支払い方法を無効のままにし、設定フィールドはすべて入力済みにしておきます。
