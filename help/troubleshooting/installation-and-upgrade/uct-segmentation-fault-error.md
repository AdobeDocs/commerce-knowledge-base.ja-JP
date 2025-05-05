---
title: アップグレード互換性ツールのエラーのトラブルシューティング
description: この記事では、アップグレード互換性ツールの使用中に発生する可能性のあるエラーについて説明し、ツールを正常に実行できるようにこれらのエラーを修正するソリューションを提供します。
exl-id: 1cce1146-942e-46cb-a395-8da9e472cd39
feature: Customer Service, Install, Upgrade
role: Developer
source-git-commit: 35d4f2130d0ec71f71f5f20aa8a7c76207e7a35a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# アップグレード互換性ツールのエラーのトラブルシューティング

この記事では、アップグレード互換性ツールの使用中に発生する可能性のあるエラーについて説明し、ツールを正常に実行できるようにこれらのエラーを修正するソリューションを提供します。

## 影響を受ける製品とバージョン

* [ 互換性アップグレードツール ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/overview.html?lang=ja) は、2.3.0 以降のAdobe Commerce バージョンと互換性があります。

## セグメント化の失敗エラー

<u> 原因 </u>:

2 つのモジュールの名前が同じ場合、アップグレード互換性ツールはセグメント化フォールトエラーを表示します。

<u> 解決策 </u>:

このエラーを回避するには、モジュールへのパスを引数として指定することをお勧めします。

```bash
bin/uct upgrade:check --current-version=2.4.4 path/to/the/module
```

>[!WARNING]
>
> メソッド間に循環依存関係がある場合、アップグレード互換性ツールはコードベースを分析できない可能性があります。

## 空の出力

<u> 再現手順 </u>:

1. このコマンドを実行した後の場合：

   ```bash
   bin/uct upgrade:check INSTALLATION_DIR -c M2_VERSION
   ```

1. 唯一の出力は `Upgrade compatibility tool` です。

   ```bash
   bin/uct upgrade:check /var/www/project/magento/ -c 2.4.1
   Upgrade compatibility tool
   ```

<u> 原因 </u>:

考えられる原因は、PHP のメモリ制限です。

この PHP のメモリ制限を回避するには、2 つの解決策が考えられます。

<u> ソリューション 1</u>:

`memory_limit` を `-1` に設定して、メモリ制限を上書きします。

```bash
php -d memory_limit=-1 /bin/uct upgrade:check INSTALLATION_DIR -c M2_VERSION
```

>[!NOTE]
>
> `M2_VERSION` は、Adobe Commerce インスタンスと比較するターゲット Adobe Commerceのバージョンです。

<u> ソリューション 2</u>:

`-m` オプションを追加すると、アップグレード互換性ツールで個々の特定のモジュールを個別に分析できるので、Adobe Commerce インスタンスで同じ名前の 2 つのモジュールが発生するのを回避できます。

また、このコマンドオプションを使用すると、アップグレード互換性ツールで、複数のモジュールを含むフォルダーを分析することもできます。

```bash
bin/uct upgrade:check /<dir>/<instance-name> -m /vendor/<vendor-name>/
```

コマンドラインインターフェイスオプションについて詳しくは、[ コマンドラインインターフェイスでのツールの実行 ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/use-upgrade-compatibility-tool/run.html?lang=ja) ページを参照してください。
