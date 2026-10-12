---
title: Cloud Pro アーキテクチャで、Database auto_increment incrementの増分変数を「3」のAdobe Commerceに設定
description: これは、3 ノードアーキテクチャが原因でAdobe Commerce on cloud infrastructure Pro プランアーキテクチャソリューションで期待される動作であり、変更できません。
exl-id: ea478cbc-2dc2-41c9-8ea7-7e2f308e5948
feature: Cloud
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%
---
# Cloud Pro アーキテクチャで、Database auto_increment incrementの増分変数を「3」のAdobe Commerceに設定

これは、3 ノードアーキテクチャが原因でAdobe Commerce on cloud infrastructure Pro プランアーキテクチャソリューションで期待される動作であり、変更できません。

Galera データベースクラスターが使用されます。これは、ノードごとに1つのMariaDB MySQL データベースを持つデータベースクラスターで、各データベース全体の一意のIDに対して3つの自動増分設定を持ちます。

<u>Pro クラスターで使用される増分IDが、必ずしも3で分離または増分されないのはなぜですか？</u>

Galeraの仕組みにより、クラスターで使用される増分IDが常に3で分離/増分されるわけではありません。

3つのサーバーはそれぞれ独自のID スペースを管理し、使用される増分は、どのMySQL メインデータベースサーバー（相対負荷に応じて）であるかによって異なるため、ギャップが異なります。
各ノードにSSH接続し、そのノードで実行されているローカル MySQL インスタンスにポート 3307を使用して接続する場合（標準ポート 3306の「main」にプロキシするのではなく）、次の図が表示されます。

![auto_increment](assets/auto_increment_id.png)

例えば、選択されたメインが`auto_increment_offset = 1`のノード 1である場合、IDは1増加します。 次に、後で新しいメインノードが選択された場合（例：`auto_increment_offset = 3`のノード 3）は、代わりに3ずつ増加します。

## 便利なリンク

アドビの開発者向けドキュメントをご覧ください。

* [Cloud for Adobe Commerce > Pro アーキテクチャ > バックアップと災害復旧](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/architecture/pro-architecture#backup-and-disaster-recovery)
* [Cloud for Adobe Commerce/前提条件のインストール：database](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/overview)
