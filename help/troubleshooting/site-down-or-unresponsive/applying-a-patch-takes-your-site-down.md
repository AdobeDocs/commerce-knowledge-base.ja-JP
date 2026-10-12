---
title: パッチを適用すると、サイトがダウンする
description: この記事では、適用したパッチがサイトをダウンさせる問題について説明します。 これを解決するには、パッチを削除します。
exl-id: dc765bcd-0761-4efd-a345-46a908d61272
feature: Cache
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%
---
# パッチを適用すると、サイトがダウンする

この記事では、適用したパッチがサイトをダウンさせる問題について説明します。 これを解決するには、パッチを削除します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）、サポートされているすべてのバージョン
* Magento Open Source、すべてのバージョン

## イシュー

パッチを適用すると、サイトがダウンします。

## 原因

この問題は、web サイトに適用したパッチ、カスタマイズ、過去に適用した他のパッチ、またはその他のエラーが原因で発生する場合があります。

## Solution

パッチを削除します。 パッチの削除方法は、Adobe Commerce オンプレミスおよびMagento Open Sourceとは異なります。

### Magento Open Source、すべての1.X バージョン

Magento Open Source 1.X バージョンの場合、

* 次のSSH コマンドを実行します：`h SUPEE_patch --revert `

### Adobe Commerce オンプレミス、Magento Open Source、すべての2.x バージョン

Adobe Commerce オンプレミスおよびMagento Open Source 2.x バージョンの場合、

1. 次のSSH コマンドを実行します。

   ```
   patch -p1 -R %patch_name%.composer.patch
   ```

   （上記のコマンドが機能しない場合は、`-p1`ではなく`-p2`を使用してみてください）

1. 変更を反映するには、**システム**/**キャッシュ管理**&#x200B;の下の管理者のキャッシュを更新します。

### Adobe Commerceオンクラウドインフラストラクチャ（全バージョン）

Adobe Commerceのクラウドインフラストラクチャには、すべてのバージョン，

1. `m2-hotfixes` ディレクトリから`%patch_name%.composer.patch` ファイルを削除します。
1. コード変更をコミットしてプッシュします。

   ```
   git commit -m "Remove %patch_name%.composer.patch patch" && git push origin
   ```

## 関連トピックス

* [Adobe](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/how-to-apply-a-composer-patch-provided-by-magento)が提供するコンポーザーパッチを適用する方法について、サポートナレッジベースを参照してください。
