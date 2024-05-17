---
title: Adobe Commerce Intelligence アカウントのロックアウトのトラブルシューティング
description: この記事では、Adobe Commerce Intelligence アカウントのロックアウトのソリューションを説明します。 最初に、これが不具合か、一時的な不具合か、その他かを判断する必要があります。 以下の手順に従うと、できるだけ早くアカウントに戻すのに役立ちます。
exl-id: 85968257-ba4b-4cfb-a4fa-497b4c5b5aea
feature: Cache, Commerce Intelligence, Console
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Adobe Commerce Intelligence アカウントのロックアウトのトラブルシューティング

<!--
BOB: Is this in TOC?
-->

この記事では、Commerce Intelligence アカウントのロックアウトのソリューションを説明します。 最初に、これが不具合か、一時的な不具合か、その他かを判断する必要があります。 以下の手順に従うと、できるだけ早くアカウントに戻すのに役立ちます。

## メールアドレスが正しいことを確認します

メールアドレスを再度確認して、ログインに使用しようとしているメールアドレスが既存のCommerce Intelligence アカウントに関連付けられていることを確認します。 場合によっては、アカウント管理者に、メールアドレスに入力ミスがないことを確認するように依頼する必要があります。

メールアドレスが正しいことを確認したら、を使用して再度ログインしてみてください。 [このリンク](https://dashboard.rjmetrics.com/v2/session/create#/).

## パスワードをリセットしてみてください

正しいメールアドレスを使用していることを確認した場合は、パスワードをリセットしてみてください。 を使用できます **忘れた？** 前の節のログインページにあるリンクから、パスワードリセットメールをトリガーします。

最初にメールが表示されない場合は、迷惑メール フォルダーを確認してください。 善意のメールでも、迷惑メールと間違えられることがあります。 **これらのメールに記載されている一時的なアクセスリンクは、1 回だけ有効であることに注意してください。**

それでもロックアウトされている場合は、メールアドレスが正しく、リセットメールの正しいリンクを使用していることを確認します。 以下を試すことをお勧めします **別のリセットを要求してログインを再試行する前に、次の操作を行います。**

* ブラウザーのキャッシュ、Cookie および保存されたパスワードをクリアします
* 広告ブロックソフトウェアを一時的に無効にする

## エラーを文書化し、サポートに連絡します。

>[!NOTE]
>
>この手順は必ずしも必要ではありませんが、事前に完了させることで、サポートリクエストに前後して費やす時間を短縮できます。

それでもアカウントにアクセスできない場合は、エラーを確認し、サポートチームにチケットを送信することをお勧めします。 これはどうすれば実行できますか。 ブラウザーの開発者ツールを開き、コンソールまたはサイトログウィンドウに表示されるエラーのスクリーンショットを撮る。 以下のGIFで、Google Chrome 用のデベロッパーツールを開きます。

![Chrome のデベロッパーツールを開く。](assets/Opening_Chrome_dev_tools.gif)

上記の例では、最も一般的なメソッド（**右クリック** > **Inspect**）を選択して、コンソールを開きます。 ブラウザーにこの方法がない場合やヘルプが必要な場合は、使用している web ブラウザーに対応する以下のドキュメントリンクを使用します。

<table>
<tbody>
<tr>
<td><a href="https://www.technipages.com/mac-os-x-enable-web-inspector-in-safari">Safari</a></td>
<td><a href="https://developer.mozilla.org/en-US/docs/Tools/Web_Console/Opening_the_Web_Console">Firefox</a></td>
<td><a href="https://developers.google.com/web/tools/chrome-devtools/?hl=en">Chrome</a></td>
<td><a href="https://www.opera.com/dragonfly/documentation/">Opera</a></td>
<td><a href="https://msdn.microsoft.com/en-us/library/gg589512(v=vs.85).aspx#OpeningTools">Internet Explorer</a></td>
</tr>
</tbody>
</table>

ブラウザーによっては、デベロッパーツールを開いても自動的にコンソールが表示されず、サイトのコードが最初に表示される場合があります。 この問題が発生した場合は、開発者ウィンドウの「コンソール」オプションをクリックし、表示されているエラーのスクリーンショットを撮ります。

サポートチームに次の情報を含むチケットを送信します： **エラースクリーンショット** および **Commerce Intelligence アカウントのメールアドレス**.

## エラーが表示されないか、単に失われているだけですか？

心配しないで。 新しいサポートチケットを申請すると（Commerce Intelligence アカウントのメールアドレスを必ず含めてください）、できるだけ早くアカウントに戻ります。

## サポートナレッジベースの関連トピック：

* [新しいユーザーの追加と権限の設定](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/administrator/user-mgmt/user-management.html)
* [メールアドレスやパスワードを更新するにはどうすればよいですか？](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/administrator/user-mgmt/create-user.html)
* [パスワードをリセットするにはどうすればよいですか？](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/administrator/user-mgmt/reset-password.html)
