---
title: Adobe Commerce ソフトウェアのアップデート時にGit pull origin developが失敗する
description: この記事では、「git pull origin develop」を実行しているときにAdobe Commerce ソフトウェアを更新できない場合の修正について説明します。
exl-id: b133253e-c160-4f15-a9b0-8591e93a1e9b
feature: Upgrade
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%
---
# Adobe Commerce ソフトウェアのアップデート時にGit pull origin developが失敗する

この記事では、`git pull origin develop`の実行中にAdobe Commerce ソフトウェアを更新できない場合の修正について説明します。

## 詳細

Adobe Commerce ソフトウェアを更新する手順の1つは、次を実行してローカルリポジトリを更新することです。

```bash
$ git pull origin develop
```

次のエラーが表示される場合があります。

```bash
error: Your local changes to the following files would be overwritten by merge:
<list of files>
```

上書きの対象となるファイルを見つけるには、メッセージを読むか、次のように入力します。

```bash
git status
```

次のセクションでは、提案された解決策について説明します。

### 推奨される解決策

解決策は、Adobe Commerce ファイルシステム内のファイルを意図的に変更したかどうかによって異なります。 詳しくは、次のいずれかの節を参照してください。

#### 意図的にファイルを変更した

通常の方法で手動で競合を解決します。 何をすべきかわからない場合は、[GitHub help](https://help.github.com/)を参照してください。

#### 故意にファイルを変更したわけではありません

次のいずれかを試します。

* ファイルを変更していないことが確実で、Adobe Commerce ファイルシステムの変更内容を削除または上書きする必要がない場合は、次のように入力します。

  </p>
    <pre><code class="language-bash">$ git reset --hard HEAD && git pull origin develop</code></pre>

  その後、Adobe Commerceのアップデートで中断したところから続行します。

* GitHub設定を使用すると、将来これらのエラーを防ぐことができます。 デフォルトでは、GitHubはオペレーティングシステムのデフォルトの行末文字を使用してコンテンツを保存します。 Linuxを使用していても、別の共同作業者がWindowsを使用して変更をコミットした場合、GitHubは、クローンまたはプル時にWindowsの行の末尾をLinuxに変換します。 これにより、実際に変更が行われなかった場合に、ファイルに変更が加えられたように見えます。

  行の終わりを無視するようにGitHubを設定するには、Git クライアントで次のコマンドを入力します。

  </p>
    <pre><code class="language-bash">$ git config --system core.autocrlf false</code></pre>

  Windowsを使用する場合は、次のように入力します。

  </p>
    <pre><code class="language-bash">$ git config --system core.eol LF</code></pre>

  >[!NOTE]
  >
  >Adobeは、特定のGitHub設定を推奨または推奨するものではありません。 上記は推奨事項のみです。 詳細については、[GitHub help](https://help.github.com/)を参照してください。

  Adobe Commerceのアップデートで中断したところから続行します。
