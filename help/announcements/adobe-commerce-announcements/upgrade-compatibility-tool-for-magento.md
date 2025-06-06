---
title: Adobe Commerce用互換性ツール 1.1.0 のアップグレード
description: アップグレード互換性ツール 1.1.0 は、Adobe Commerceのカスタマイズ済みインスタンスにインストールされているすべてのモジュールとコアコードを分析し、インスタンスを特定のバージョンと照合するコマンドラインツールです。 Adobe Commerceの最新バージョンにアップグレードする前に対処する必要がある重要なエラー、問題、警告のリストを返します。
exl-id: 312abc5a-1d6a-4f32-9929-a94f4962eddd
feature: Upgrade
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Adobe Commerce用互換性ツール 1.1.0 のアップグレード

アップグレード互換性ツール 1.1.0 は、Adobe Commerceのカスタマイズ済みインスタンスにインストールされているすべてのモジュールとコアコードを分析し、インスタンスを特定のバージョンと照合するコマンドラインツールです。 Adobe Commerceの最新バージョンにアップグレードする前に対処する必要がある重要なエラー、問題、警告のリストを返します。

## UCT 1.1.0 の新機能

アップグレード互換性ツール 1.1.0 では、次のような大幅な改善が導入されています。

* **コアファイルの変更を検証**:Adobeでは、コア製品コードのカスタマイズを行うことを強くお勧めします。 このリリースでは、お客様およびパートナーがコアコードの変更を特定して変更の影響を早期かつ迅速に把握できるように、チェックポイントを追加しました。 開発プロセスにこのツールを追加することで、パートナーやマーチャントがプロアクティブに問題を特定し、将来のアップグレード時の問題を防ぎ、総所有コスト（TCO）を削減できるようになります。
* **レポートを JSON ファイルに書き出す**：この改善は、コミュニティからのフィードバックに従って実装されました。 現在は、ツールを実行すると、特定されたすべての問題の詳細が JSON ファイルに書き出されるので、ユーザーはツールを再度実行しなくても結果を読み取り、共有、管理できます。
* **VBE 検証の改善**: VBE （ベンダーバンドル拡張機能）は、Adobe Commerce コアコードの一部ではなく、Adobeでテストおよびサポートされています。 この更新では、コアコードと同じアプローチを使用して VBE を検証するようになりました。 この改善により、カスタマイズとコアコード/VBE に関連する問題を明確に理解できるようになります。
* **エラーコードの提供**：ユーザーがアップグレード中の問題を識別、理解、解決するのに役立つエラーコードを導入しました。 エラーおよび警告メッセージは、明確な説明と解決策を提供します。
* **重要な問題のみをリストアップ可能**：これにより、ユーザーは重要な問題にのみ集中でき、アップグレード中に問題が発生します。
* **2 つのバージョン間の差分イシュー**：コミュニティメンバーが提案するこの改善により、UCT ユーザーは、2 つのバージョン間のイシューの差分を取得できます。これにより、アップグレードするターゲットバージョンに導入された新しいイシューにのみ焦点を当てることができます。

## ツールで比較できるバージョンはどれですか？

このツールを使用すると、任意の 2.x バージョンを比較できます。

## アップグレード互換性ツール 1.1.0 を使用できるユーザー

Adobe Commerceのお客様。

## アップグレード互換性ツール 1.1.0 のインストール

インストールの手順については、開発者向けドキュメントのAdobe Commerce:[ 互換性ツールをアップグレード/インストール ](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/use-upgrade-compatibility-tool/run) を参照してください。 このツールを使用するための前提条件については、開発者向けドキュメントのAdobe Commerce：互換性ツールのアップグレード [&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/prerequisites) を参照してください 

## 各問題の横にある数字は何ですか？

アップグレード互換性ツールの実行中に発生する可能性のあるエラーに関する情報を提供するエラーメッセージ リファレンスです。

アップグレード互換性ツールのエラーメッセージは、レベル（重大な問題、エラー、警告）およびタイプ（コアコード、カスタムコード、GraphQL スキーマ）ごとに分類されます。 各タイプには、次の情報が含まれます。

* エラーコード：エラーメッセージにAdobe Commerceによって割り当てられた識別情報。
* エラーの説明：エラーの原因の概要を示す説明。
* エラーの推奨アクション：該当する場合は、エラーのトラブルシューティングと解決に関するガイダンスを提供します。
* コードのリストと説明については、[ エラーメッセージ参照ページ ](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/reporting/error-messages) を参照してください。

## ツールに関するフィードバックはどこで共有できますか？

UCT の [#upgrade-compatibility-tool](https://magentocommeng.slack.com/archives/C019Y143U9F) Slack チャンネルで UCT チームに連絡してください。 ツールを改善するためのフィードバックや提案をお待ちしています。

## 関連資料

* Adobe Commerce ブログ：[ アップグレード互換性ツール（Alpha）の概要 ](https://magento.com/blog/magento-news/introducing-upgrade-compatibility-tool)
* Adobe Commerce：開発者向けドキュメントの [ 互換性アップグレードツール ](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/overview)。
