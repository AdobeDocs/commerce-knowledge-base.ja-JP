---
title: Adobe Commerce リリースの更新されたライフサイクルポリシーに関する FAQ
description: 「Adobe Commerceは、次回のマイナーソフトウェアリリースの一般提供日から少なくとも 12 か月間、マイナーリリースの品質修正を提供します。 この間に私たちが品質修正を提供する方法は変わりつつあります。」
exl-id: 4aa601d0-ee1d-4f1f-a684-188772a58dd1
feature: Compliance, Support
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 0%

---

# Adobe Commerce リリースの更新されたライフサイクルポリシーに関する FAQ

## 何が変わってるの？

Adobe Commerceは、次のマイナーソフトウェアリリースの一般提供日から少なくとも 12 か月間、マイナーリリースの品質修正を提供します。 この間にアドビが提供する品質の修正の方法は変化しています。

* **以前のポリシー：** 現在、12 か月の EOS ウィンドウにある前の行に対する品質修正は、四半期ごとのパッチリリースを通じて提供されているため、四半期ごとのパッチはセキュリティと品質の組み合わせになります。
* **新規ポリシー：** 最新のマイナーリリース行として 2.4 以降、以前のサポートされている行（2.3）のリリースパッチはセキュリティ専用に移行されます。 マイナーリリース後の 12 か月間（2.4 など）、および後続の新しいマイナーリリースラインでは、以前サポートされていたラインの品質修正を引き続き提供しますが、それらはで利用できるようになります。 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 重要な問題にのみ焦点を当てる。

## このポリシーはいつ有効になりますか？

Adobe Commerce 2.3.6 は 2020 年 10 月 15 日（PT）にリリースされる予定で、品質とセキュリティの両方を含むAdobe Commerce 2.3 の最後のパッチリリースになる予定です。 2.3.6 以降、2.3.x 回線はセキュリティ専用になり、2.3 の重大な品質問題は QPT を通じて修正できます。

>[!NOTE]
>
>2.3 のフルバージョンをリリースするのは、PHP やElasticsearchなどのテクノロジースタックへの準拠を維持する必要がある場合のみです。 この問題は 2021 年第 2 四半期に発生しており、PHP 7.4 の必須アップデートに伴い、2.3.7 行目まで増分する予定です。詳しくは、こちらを参照してください。 [Adobe Commerce 2.3.x リリース行の PHP 7.4 のサポート](https://community.magento.com/t5/Magento-DevBlog/PHP-7-4-support-for-Magento-2-3-x-release-line/ba-p/458946) DevBlog の投稿。

## セキュリティのみのリリースとは何ですか？

セキュリティのみのリリースには、セキュリティの修正のみが含まれており、品質の修正は含まれていません。 ただし、Adobe Commerceを実行するために絶対に重要であると考えられる場合は、セキュリティ専用リリースに特定のホットフィックスが含まれる可能性があることに注意してください。

## 最新の行（公開 2.4 時点）については、セキュリティのみのリリースが残っていますか？

Adobeでは、最新のリリースラインに対しても引き続きセキュリティのみのリリースを用意しています。 これらのプロセスの概要については、を参照してください。 [新しいセキュリティ専用パッチリリースの導入](https://community.magento.com/t5/Magento-DevBlog/Introducing-the-New-Security-only-Patch-Release/ba-p/141287) DevBlog の投稿。

## 品質向上パッチツールとは

を参照してください [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースの記事

## この新しいポリシーの使用を検討するユーザー

この新しい方針は、マーチャントが年間Adobe Commerce開発コストを戦略的に計画する道筋を作り出すと同時に、これらの戦略的サイクルの間にセキュリティと重要な品質を維持できるようにすることを目的としています。 また、他のすべてに対するセキュリティを重視し、一般的に古いサポート対象ラインの安定性に満足しているマーチャントも利用できます。 マーチャントは、これらのアップグレードの計画と予算を立てるのが簡単になる場合があります。これは、アップグレードの予測可能性が高くなるからです。

## マーチャントは最新のラインにアップグレードする必要がありますか？

最終的に、すべてのマーチャントは、最新のAdobe Commerceラインをタイムリーに採用する計画を優先する必要があります。 新しいセキュリティのみのラインと QPT ツールは、マーチャントの戦略的アップグレードロードマップに取って代わることを目的としていません。むしろ、マーチャントがアップグレードロードマップを計画する際に柔軟性を提供し、アップグレード全体を実装する必要なく、セキュリティと品質の問題に迅速に対応する手段を提供します。

## サポートされているマイナーバージョンで最新の行ではない品質修正を取得するにはどうすればよいですか？

修正は、次から利用できるようになります [品質向上パッチツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md).

## 最新のラインで品質の修正を受けるにはどうすればよいですか？

現在のラインは、四半期ごとの更新の一環として品質を持ちます。 リリースの間に、最新の回線の修正についてサポートに連絡すると、QPT 経由で提供されます。 その後、その修正を含むリリースにアップグレードすると、四半期ごとのパッチで適用されます。

## サポートされている最新のマイナーバージョン以外のマイナーバージョンでは、どのような品質の問題が修正されますか？

前の行（2.3）で修正し、QPT を介して配信されるのは、コアフローを損なう重大な品質問題のみです。

## 最新の行ではないサポート対象のマイナーバージョンの四半期リリースに、品質の修正は含まれていますか？

はい、セキュリティ専用ラインの一部として、Adobeが「ホットフィックス」と呼ぶものをリリースしています。これらは、Adobe Commerce アプリケーションに影響を与える非常に重要な問題です。

## セキュリティの向上と QPT は同時に提供されますか？

セキュリティ専用のラインは、四半期ごとのリリーススケジュールに従い、-p1 の命名法でリリースされます。 例 2.3.6-p1 品質の問題が発見され、修正されると、その場で品質がリリースされ、QPT を通じて利用可能になります。

## 最新の行や QPT ではないサポート対象のマイナーバージョンでは解決されない品質の問題がある場合は、どうすればよいですか？

前の行はセキュリティのみであるため、主なメリットはセキュリティを維持することです。 コアフローを中断する重大な問題に対するパッチのみが、QPT を通じて提供されます。

コアフローに影響を与えない問題や回避策のある問題は、最新の行でのみ修正されます。 Adobeは、重要な修正と重要でない修正の両方を希望する場合は、最新の行に移動することをお勧めします。

## マーチャントがセキュリティサポートの終了までセキュリティ専用ラインにとどまっている場合、アップグレードは高価になるか、困難になりますか？

理論的には、多数の品質パッチを採用していない限り、開発時間の点でマーチャントのコストは等しくなければなりません。 マーチャントが QPT ツールを使用して少数のパッチが必要または必要であると判断した場合、最新バージョンのAdobe Commerceへのアップグレードを優先することをお勧めします。 現在のAdobe Commerceのバージョンにアップグレードする代わりに、多数のクオリティパッチを適用すると、セキュリティ専用線がサポート終了に達した場合の開発コストの増加やアップグレードの複雑さの増大を招く可能性があります。

## QPT 経由で提供される品質パッチの量を制限する必要があるのはなぜですか。

個別の品質に関する多数の修正を適用すると、Adobe Commerce コードがより複雑になります。 複雑さが追加され、最新のリリースラインにアップグレードする際に、予期しない変更が発生する可能性があります。 そのため、QPT は慎重に、最も重要な修正に対してのみ使用することをお勧めします。

## テクノロジースタックのコンプライアンスについてはどうですか？

リリースラインの有効期間中に、PHP やElasticsearchなどの様々なテクノロジースタックを更新し、準拠を維持するためにアップグレードする必要があります。 私たちは、これらの来ていることを私たちの商人にできるだけ多くの通知を与えます。

注意：2021 年の第 2 四半期に、2.3.x 行で PHP と Redis を更新して、準拠を維持する必要があります。 これにより、行が 2.3.7 に増加します。詳しくは、こちらを参照してください。 [Adobe Commerce 2.3.x リリース行の PHP 7.4 のサポート](https://community.magento.com/t5/Magento-DevBlog/PHP-7-4-support-for-Magento-2-3-x-release-line/ba-p/458946) DevBlog の投稿。